## File Processing with Redis


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
	
	#Print the line nicely formatted
    #print json.dumps(line, sort_keys=True,indent=4, separators=(',', ': '))

	
    #for key in line:
        #print key,'=>',line[key],type(line[key])
    for nut in line['nutrients']:
    	r.hmset(nut['_id'],nut)
        r.rpush(nut['tagname'],nut)
        
    #sys.exit(0)
    #r.hmset(line['_id'],line)

```
