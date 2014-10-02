#### Not Complete
## File Processing with Redis

### Commands

- `redis-cli` 
    - Opens the command line interface to redis.
- `info`
    - Gives information about server including disk usage.
- `flushall`
    - Cleans out the entire database ! 



Python will kill process when `sys.exit(0)` encountered. This can be used for testing purposes 
to stop a process after an iteration or two.

```python

   import sys
   
   sys.exit(0)
```

Python example of opening a file, read every line, printing every line

```python
import string

# Open file for reading
f = open('nutrition.txt', 'r')

# Read every line from file and print it
for line in f:
    print line
       
```

Loop through a python dictionary

```python
    # loops through a dictionary and prints out
    # every key value pair
    for key in dict:
        print key,'=>',dict[key],type(dict[key])
```

Print json nicely with line returns and indentation

```python
    #Print the line nicely formatted
    print json.dumps(line, sort_keys=True,indent=4, separators=(',', ': '))
```

```python
#r.hmset(line['_id'],line)
```


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
