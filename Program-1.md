# Not Done
## Program 1 - Getting Our Feet Wet

### Basic Idea
In class we've mainly discussed basic generalities describing and dealing with the whole "Big Data" concept.
So, for this programming project, we will get a small taste of dealing with  (relatively) big data. More specifically we
will deal with converting a large set of data from one format to another. 

In an academic setting, it's very typical that programming assignments may solve difficult problems, but solve
them very quickly! Meaning the implementation of a complex data structure may be conceptually difficult, but
when it comes to running or testing your program, it usually uses a very small data set, and if it runs any longer
than a few seconds, you think it's broken and possibly in an endless loop. Well that is about to stop. 

### Background

You are given a set of GPS data points. Actually, your given the same set of GPS data points in multiple
formats:

```bash
-rw-rw-r--  1 griffin griffin 484M Sep  2 17:20 GpsFilePoints.csv
-rw-rw-r--  1 griffin griffin 467M Sep  2 17:22 GpsFilePoints.sql
-rw-rw-r--  1 griffin griffin 2.3G Sep  2 17:24 GpsFilePoints.xml
-rw-rw-r--  1 griffin griffin 771M Sep  2 17:24 GpsFilePoints.yml
```

As seen in the directory listing above we have the following files:

| Type | Description                                  | Size    |
|------|----------------------------------------------|---------|
| csv  |Comma seperated values                        | 484MB   |
| sql  |Structured Query Language (insert statements) | 467MB   | 
| xml  |EXtensible Markup Language                    | 2.3GB   |
| yaml |Yet Another Markup Language                   | 771MB   |
| json |Javascript Object Notation                    | ?       |

Each format has it's benefits, and detractors. Also, as you can see, we are missing the JSON file format. 

You will need one or more of the files to complete your assignment. To gain access to the files 
you can use the following link: 

http://cs.mwsu.edu/~griffin/5443-BigData

## Requirements

### One

Convert any one of the above files into a `json` representation. Do this on your own server using the `python` 
scripting language. I realize that most of you have zero `python` experience, but that's the fun of it.

Start with installing python:

```bash
sudo apt-get install python3
```

Here is an example python snippet to convert from csv to json:

```python
import csv
import json

csvfile = open('file.csv', 'r')
jsonfile = open('file.json', 'w')

fieldnames = ("FirstName","LastName","IDNumber","Message")
reader = csv.DictReader( csvfile, fieldnames)
for row in reader:
    json.dump(row, jsonfile)
    jsonfile.write('\n')
```

#### Scenario

Your a programmer that needs to simply transmit the 

In the following scenario, 

- Describe the benefits of each file format. 
- Give examples of when a file format would be detrimental. 
- Is any one format more of a robust solution than the others.
 

 
