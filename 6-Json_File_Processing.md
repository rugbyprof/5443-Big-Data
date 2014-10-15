## File Cleansing and Loading

This is a small walk through that prepares us to use php to load json data into a `Redis` key value store. As of now, it's really an assignment to remove the "bad" characters that are plaguing our json data. After we get over that hurdle, then we can load the data into `Redis`.

### What you need to accomplish

- On your server add a user called `redis`

```
$ useradd redis
```

- In `/home/redis` create a folder called `data` and copy `nutrition.json` into that folder (http://107.170.214.232/nutrition.json)
- You can split `nutrition.json` if you like, or leave it at `65mb`.
- Create a script called `process_json.???` replacing the `???` with whatever scripting language you use (php, py, etc.) and place it in `/home/redis`.
- When I run your script, it should process `nutrition.json` (or the smaller split files) and do the following:
    - Remove any characters that are not ascii (subset of UTF-8).
    - Display the illegal characters with the line number where it was found.
    - Display how many lines processed in total.
    - Display how many characters removed.
    - Display the list of unique characters removed (I think it's one).
- Thier are a couple of snippets at the _bottom_. One in Php and one in Python. Neither is a solution, just some code to give you an idea of where to start.

Directly below are some helpful resources:

### Installing Redis

- Here is a Digital Ocean tutorial on installing Redis:

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-redis

- In addition, you need to install php5-dev on your server 

```bash
sudo apt-get update

sudo apt-get updgrade

apt-get install php5-dev
```

- Clone the following repository onto your server:

https://github.com/nicolasff/phpredis.git

Then `cd phpredis` (change into the directory you just cloned).

```
sudo phpize5

sudo ./configure

sudo make 

sudo make test

sudo make install
```

### Some helpful links

- Json Decode
    - http://de2.php.net/manual/en/function.json-decode.php
- Check Character Encoding
    - http://php.net/manual/en/function.mb-detect-encoding.php
- Split file into so many lines
    - split -l 500 myfile segment
- Json validator web site
    - http://jsonlint.com/
- sed command to print line out of middle of file
    - http://www.commandlinefu.com/commands/view/3802/to-print-a-specific-line-from-a-file
- Ptyhon examples
    - http://stackoverflow.com/questions/8689795/python-remove-non-ascii-characters-but-leave-periods-and-spaces
    
### Python Helper Snippet 

```php
import redis
import string
import json
import sys

#Link up with redis
r = redis.Redis(host='localhost', port=6379, db=0)

f = open('nutrition.json','r')
# Read one line from file

for line in f:
    # Filter that line, removing non ascii characters
    # Doesn't identify which, just filters
    line = json.loads(filter(lambda x: x in string.printable, line))

    #Print the line nicely formatted
    #print json.dumps(line, sort_keys=True,indent=4, separators=(',', ': '))

```
