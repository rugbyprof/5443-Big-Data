### Assignment 4 - Key Value Stores / Document Stores


#### Quiz on Tue Sep 23<sup>th</sup>
-----

Below are the highlights to 2 tutorials that cover `Redis` and `MongoDB`. These are a couple of popular `noSql` databases. Since `SQL` typically corresponds with `Relational Databases`, and this type of database is not known for its scalability, we will look into `Redis`: A key/value store database, and `MongoDB`: a document database.

## MONGODB

http://try.mongodb.org/

### Js Objects
- var a = {"fname":"Joe","lname":"Smith","age":20,"languages":['C++','Ruby','Python','Php']}


### DB 
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


## REDIS


http://try.redis.io/

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

