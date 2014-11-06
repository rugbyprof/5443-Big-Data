### Assignment 4 - Key Value Stores / Document Stores Overview

-----

Below are the highlights of tutorials that cover `Redis` and `MongoDB`. These are a couple of popular `noSql` databases. Since `SQL` typically corresponds with `Relational Databases`, and this type of database is not known for its scalability, we will look into `Redis`: A key/value store database, and `MongoDB`: a document database, both of which don't use `SQL` to query thier data.

Here are the links to each tutorial:

- http://try.mongodb.org/
- http://try.redis.io/

I've provided the highlights below, mostly so you know what to study for our quiz on Tuesday the 23<sup>rd</sup>. We will meet in room 103 and you will work directly on your server. I will have you load some data, then query that data using either MongoDB or Redis or both. The query's will not get complex, but you should have an idea of what each of the key words listed below are.

Prior to Tuesday, you will need to install MongoDB and Redis on your server.Links provided to both installation tutorials below.

## MONGODB

- http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/
- http://docs.mongodb.org/manual/tutorial/getting-started/

### Json Objects
- {} = object
- [] = array
- var a = {"fname":"Joe","lname":"Smith","age":20,"languages":['C++','Ruby','Python','Php']}


### DB. Commands
- .save()
- .find()
  - $gt
  - $gte
  - $lt
  - $ne
  - $in
- .update()
  - $addToSet
  - $set
  - $push
  - $pull
- .remove()

-----

## REDIS

- https://www.digitalocean.com/community/tutorials/how-to-install-and-use-redis

### Lists
- http://redis.io/commands#list
- RPUSH
- LPUSH
- LLEN
- LRANGE
- LPOP
- RPOP

### Sets
- http://redis.io/commands#set
- SADD
- SREM
- SISMEMBER
- SMEMBERS
- SUNION.

### Sorted Sets
- http://redis.io/commands#sorted_set
- ZADD
- ZRANGE

### Hashes
- http://redis.io/commands#hash
- HSET
- HGETALL
- HMSET 
- HGET 
- HINCRBY
- HDEL

