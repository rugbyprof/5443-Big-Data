## File Processing with Redis

### Commands

- `redis-cli` 
    - Opens the command line interface to redis.
- `info`
    - Gives information about server including disk usage.
- `flushall`
    - Cleans out the entire database ! 

### Redis keys

A note on naming conventions for keys in redis. Taken from [here](http://redis.io/topics/data-types-intro):
>Redis keys are binary safe, this means that you can use any binary sequence as a key, from a string like "foo" to the content of a JPEG file. The empty string is also a valid key.<br>
__A few other rules about keys:__
- Too long keys are not a good idea, for instance a key of 1024 bytes is not a good idea not only memory-wise, but also because the lookup of the key in the dataset may require several costly key-comparisons. Even when the task at hand is to match the existence of a big value, to resort to hashing it (for example with SHA1) is a better idea, especially from the point of view of memory and bandwidth.
- Too short keys are often not a good idea. There is little point in writing "u1000flw" as key if you can write instead `user:1000:followers`, the latter is more readable and the added space is little compared to the space used by the key object itself and the value object. However it is not possible to deny that short keys will consume a bit less memory. Your job is to find the right balance.
- Try to stick with a schema. For instance `object-type:id` can be a nice idea, like in `user:1000`. Dots or dashes are often used for multi-words fields, like in `comment:1234:reply.to` or `comment:1234:reply-to`.
- The maximum allowed key size is 512 MB.

Python will kill process when `sys.exit(0)` encountered. This can be used for testing purposes 
to stop a process after an iteration or two.

```python

   import sys
   
   sys.exit(0)
```

Python example of opening a file, read every line, printing every line

```python
# Open file for reading
f = open('nutrition.txt', 'r')

# Read every line from file and print it
for line in f:
    print line
       
```

Python example of opening a file, read every line as json, printing it out nicely

```python
import json

# Open file for reading
f = open('nutrition.txt', 'r')

# Read every line from file and print it
for line in f:
    #Read line in as json
    dict = json.loads(line)
    
    #Print the line nicely formatted
    print json.dumps(dict, sort_keys=True,indent=4, separators=(',', ': '))
       
```

Loop through a python dictionary

```python
    # loops through a dictionary and prints out
    # every key value pair
    for key in dict:
        print key,'=>',dict[key],type(dict[key])
```

### Redis commands via Python

```python
#First you must import redis, and establish a link
import redis
r = redis.StrictRedis(host='localhost', port=6379, db=0)
```
-----

Given the following python dictionary:

```python
phone = {'griffin': 4439, 'stringfellow': 4139,'passos':4444,'donovan':4431,'johnson':4355,'simpson':4356,'wuthrich':4664, 'halverson':4988}
```

```python
#Set single key value
r.set('griffin',phone['griffin'])
```

```python
#Set multiple key values
for key in phone:
    r.set(key,phone[key])
```

```python
#Get multiple values
for key in phone:
    print r.get(key)
```
```python
#Set multiple hash fields to single key
r.hmset('phone',phone)
```

-----

Given the following python dictionary:

```python
phonelist = {
'cs':{'griffin': 4439, 'stringfellow':4139,'passos':4444,'donovan':4431,'johnson':4355,'simpson':4356},
'bio':{'scales':5555,'Cook':5432,'Horner':5433,'Shipley':5987},
'chem':{'halford':6754,'hanson':6887,'shao':6232}
}
```

```python
#Set multiple hash fields to multiple keys
for key in phonelist:
    r.hmset(key,phonelist[key])
    
r.hgetall('cs')
```

>output `{'griffin': '4439', 'stringfellow': '4139', 'johnson': '4355', 'donovan': '4431', 'passos': '4444', 'simpson': '4356'}`

-----

More advanced example

```python
#Generate multiple hashes, and add keys to a set 
#so we can retreive all later 
for key in phonelist:
    rediskey = "phone:"+key
    r.hmset(rediskey,phonelist[key])
    r.sadd('phone',key)

#get all the members out of the phone set
#which is all the keys we used
keys = r.smembers('phone')

#Use those keys in the 'phone' set to retreive the data from our hash
for key in keys:
    r.hgetall(key)
```
Output:
```
{'griffin': '4439', 'stringfellow': '4139', 'johnson': '4355', 'donovan': '4431', 'passos': '4444', 'simpson': '4356'}
{'Cook': '5432', 'Horner': '5433', 'Shipley': '5987', 'scales': '5555'}
{'hanson': '6887', 'halford': '6754', 'shao': '6232'}
```

#### Example from class

```python
import redis
import string
import json
import sys

#Link up with redis 
r = redis.StrictRedis(host='localhost', port=6379, db=0)

# Open file for reading
#f = open('nutrition.json', 'r')
f = open('x00','r')
# Read one line from file

for line in f:
    # Filter that line, removing non ascii characters
    # Doesn't identify which, just filters
    line = json.loads(filter(lambda x: x in string.printable, line))
    
    #line is a dictionary with multiple keys, in this case we just
    #want to loop through the 'nutrient' portion
    for nut in line['nutrients']:
        #Set values in a hash with 'key' = '_id'
    	r.hmset(nut['_id'],nut)
    	#Push that hash onto a list with 'key' = 'tagname'
        r.rpush(nut['tagname'],nut)
        
```
