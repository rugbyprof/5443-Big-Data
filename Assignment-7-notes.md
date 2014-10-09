### Not Complete!

### What is MongoDB?

> MongoDB (from "humongous") is a scalable, high-performance, open source NoSQL database.

### Document database

`MongoDB` is a document database, which means that instead of storing "rows" in "tables" like a relational database, "documents" are stored in "collections."  Documents are basically `JSON` objects (technically `BSON`). This is to be distinguished from other NoSQL-type databases such as key-value cache and store (e.g. Redis).


### Document

![](http://docs.mongodb.org/manual/_images/crud-annotated-document.png)

### Collections

![](http://docs.mongodb.org/manual/_images/crud-annotated-collection.png)

### CRUD

CRUD is an acronym that stands for:  `C`reate, `R`ead, `U`pdate and `D`elete. Below are links to MongoDB's version of CRUD operations. 

http://docs.mongodb.org/manual/core/crud-introduction/
http://docs.mongodb.org/manual/core/read-operations-introduction/
http://docs.mongodb.org/manual/core/write-operations-introduction/

### Using Python with MongoDB

- If `MongoDB` is not installed, then: `sudo apt get install mongo-db`
```bash
sudo apt get install mongo-db
```

- You can install `pymongo` in a variety of ways, but this should work:

```bash
sudo apt-get install python-pymongo
```

### Grab some Data

```bash
wget http://media.mongodb.org/zips.json# -O zipcodes.json
```

### Load the Data into MongoDB

```python
import pymongo
import string
import json
import sys

def is_json(myjson):
   try:
      json_object = json.loads(myjson)
   except ValueError, e:
      return False
   return True

#Link up with mongo 
from pymongo import MongoClient
conn = MongoClient()

#Connect to your database
db = conn.MyDatabase

# Open file for reading
f = open('zipcodes.json','r')

# Read all lines from file
count = 0
for line in f:
    # Filter that line, removing non ascii characters
    # Doesn't identify which, just filters
    if is_json(line):
        line = json.loads(filter(lambda x: x in string.printable, line))
        db.zipcodes.insert( line )
        count = count + 1

print "Loaded %d documents into Mongo" % (count)
```

### Some Helpful Mongo Commands

#### General Commands

- `show dbs`  Show a list of available databases
- `use dbname` Use a spcific database
- `show collections` Show the collections within that database
- `db.dropDatabase();` Drop the database (carefull !!!)

#### Query Type Commands

- `db.collection.find()`
- `db.collection.findOne()`
- `db.keyword.find({ retweet_count : {$gte:0}},{text:1,_id:0})`

http://altons.github.io/python/2013/01/21/gentle-introduction-to-mongodb-using-pymongo/

### Twitter + Python + MongoDB

#### Create a Twitter Dev Account

- Go to https://dev.twitter.com/ and create a developer account. If you already have a twitter account, log in with your existing credentials. 
- Find the link "manage your apps" and create a new app.
- Follow the instructions. Your goal is to get an app created so you can obtain the following:
    - Consumer Key (API Key)
    - Consumer Secret (API Secret)
    - Access Token
    - Access Token Secret

#### Install Tweepy

```bash
sudo apt-get install python-tweepy
```

#### Example search Twitter for a keyword

```python
import tweepy
import pymongo
import json
import sys

from pymongo import MongoClient

def is_json(myjson):
   try:
      json_object = json.loads(myjson)
   except ValueError, e:
      return False
   return True

conn = MongoClient()
db = conn.twitter

#Twitter app info
#Replace with YOUR info!
consumer_key = '-------------------------'
consumer_secret = '-----------------------------------------------'
access_token = '--------------------------------------------'
access_token_secret = '-----------------------------------------------'

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.API(auth)    
    
keyword = 'cricket'

count = 0

tweets = api.search(keyword)
for tweet in tweets:
	#Pull out json from api
	tweet = tweet._json

	# Insert tweet
	db.cricket.insert( tweet )
	print count
	count = count + 1

```

#### Example streaming Twitter listener 

```python
from tweepy.streaming import StreamListener
from tweepy import OAuthHandler
from tweepy import Stream

import pymongo
import json
import sys

from pymongo import MongoClient

# Go to http://dev.twitter.com and create an app.
# The consumer key and secret will be generated for you after



class StdOutListener(StreamListener):
    """ A listener handles tweets are the received from the stream.
    This is a basic listener that just prints received tweets to stdout.

    """
    def __init__(self):
        self.conn = MongoClient()
        self.db = self.conn.twitter
    
    def on_data(self, data):
    	jdata =  json.loads(data)
        self.db.tweets.insert( jdata )
        return True

    def on_error(self, status):
        print status

if __name__ == '__main__':
    #Twitter app info
   consumer_key = '-------------------------'
   consumer_secret = '-----------------------------------------------'
   access_token = '--------------------------------------------'
   access_token_secret = '-----------------------------------------------'	

    l = StdOutListener()
    auth = OAuthHandler(consumer_key, consumer_secret)
    auth.set_access_token(access_token, access_token_secret)

    stream = Stream(auth, l)
    stream.filter(track=['big data','bigdata','hadoop','data mining'])
```



