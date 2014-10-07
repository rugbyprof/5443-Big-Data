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

http://docs.mongodb.org/manual/core/crud-introduction/
http://docs.mongodb.org/manual/core/read-operations-introduction/
http://docs.mongodb.org/manual/core/write-operations-introduction/

### Using Python with MondoDB

- Install mongo-db

- Install python-pymongo

```bash
sudo apt-get install python-pymongo
```

Making a Connection with MongoClient
The first step when working with PyMongo is to create a MongoClient to the running mongod instance. Doing so is easy:

```python
from pymongo import MongoClient
client = MongoClient()
```

show dbs

use dbname

show collections

db.dropDatabase();

db.collection.find()
db.collection.findOne()

