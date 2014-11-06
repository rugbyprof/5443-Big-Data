## File Cleansing and Loading

This is a small walk through that prepares us to use python to load json data into a `Redis` key value store. As of now, it's really an assignment to remove the "bad" characters that are plaguing our json data. After we get over that hurdle, then we can load the data into `Redis`.

### Background

- Create a folder called `Redis` in `/var/www/html/BigData`
- Copy nutrition.json into `Redis`

```
$ cd Redis
$ wget http://107.170.214.232/nutrition.json
```

- You can split `nutrition.json` if you like, or leave it at `65mb`, but you must process the whole file.
- Create a script called `process_json.py` and place it in `/var/www/html/BigData/redis`.

#### Installing Redis

- [Here](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-redis) is a Digital Ocean tutorial on installing Redis.
- Install [python-redis](https://github.com/andymccurdy/redis-py). The link goes to the git repository which has a decent introduction.

```bash
sudo apt-get install python-redis
```

#### Helpful resources:

- Json Library
    - https://docs.python.org/2/library/json.html
- Python filter
    - `filter(lambda x: x in string.printable, line)` # filters non ascii out of "line"
- Split file into so many lines
    - split -l 500 myfile segment
- Json validator web site
    - http://jsonlint.com/
- sed command to print line out of middle of file
    - http://www.commandlinefu.com/commands/view/3802/to-print-a-specific-line-from-a-file
- Ptyhon examples
    - http://stackoverflow.com/questions/8689795/python-remove-non-ascii-characters-but-leave-periods-and-spaces
    
### Python Snippet 

Read the comments below to understand the script, but first a little about the imports:

- `import redis` - needed to connect with our key/value store
- `import string` - needed for the filter
- `import json` - Ummm Guess!
- `import sys` - Not totally necessary, but I keep it in case I want to put a sys.exit(0) or something to stop my program at a certain point. This is only OK in dev/debug mode. Never good in production!

```php
import redis
import string
import json
import sys

#Link up with redis
r = redis.Redis(host='localhost', port=6379, db=0)

# Open nutrition.json for reading and put the reference in 'f'
f = open('nutrition.json','r')

# Read each line from f placing one line into jline at every iteration
for jline in f:
    # Filter that line, removing non ascii characters
    # Doesn't identify which, just filters
    jline = json.loads(filter(lambda x: x in string.printable, jline))

    #Print the line nicely formatted
    print json.dumps(jline, sort_keys=True,indent=4, separators=(',', ': '))

```
#### Write Up

- When I run your script, it should process `nutrition.json` and do the following:
    - Remove any ill-formed lines or characters from the dataset.
    - Display how many lines processed in total.
    - Display how many lines not processed (illegal json ... I provided a function in class to identify this).
    - Display the ratio of good vs bad lines.
    - (___BONUS___) Display the illegal characters with the line number where it was found.
    - (___BONUS___) Display how many characters removed.
    - (___BONUS___) Display the list of unique characters removed.
- As your script runs, it should create a file with the "good" json in it. Call this file: `nutrition_clean.json`
- It should also create an output file: `writeup.md` with the above information in it (in `markdown` format)

```
### Json File Processing
### Written by Your Name

- Total Lines Processed: xxxxxx
- Total Lines Remove: xx
- Ratio of Good Vs Bad: x%

### Bonus

- Illegal character "?" found on line xxx
- etc.
```

- After your done, you should have a directory structure similar to: 


-----

- ![1] /var/www/html
	- ![1] BigData
	  - ![1] FileFormats
	  - ![1] Hadoop
	  - ![1] Redis
	      - ![6] nutrition.json
	      - ![6] nutrition_clean.json
	      - ![13] process_json.py`
	      - ![9] writeup.md
	- ![9] README.md
	
-----

#### Lastly

___Push your files to GitHub___


[1]:  http://cs.mwsu.edu/~griffin/Free-file-icons/24px/folder2.png
[2]:  http://cs.mwsu.edu/~griffin/Free-file-icons/24px/php.png
[3]:  http://cs.mwsu.edu/~griffin/Free-file-icons/24px/html.png
[4]:  http://cs.mwsu.edu/~griffin/Free-file-icons/24px/css.png
[5]:  http://cs.mwsu.edu/~griffin/Free-file-icons/24px/js.png
[6]:  http://cs.mwsu.edu/~griffin/Free-file-icons/24px/json.png
[7]:  http://cs.mwsu.edu/~griffin/Free-file-icons/24px/xml.png
[8]:  http://cs.mwsu.edu/~griffin/Free-file-icons/24px/csv.png
[9]:  http://cs.mwsu.edu/~griffin/Free-file-icons/24px/md2.png
[10]: http://cs.mwsu.edu/~griffin/Free-file-icons/24px/sql.png
[11]: http://cs.mwsu.edu/~griffin/Free-file-icons/24px/yml.png
[12]: http://cs.mwsu.edu/~griffin/Free-file-icons/24px/json.png
[13]: http://cs.mwsu.edu/~griffin/Free-file-icons/24px/py.png
