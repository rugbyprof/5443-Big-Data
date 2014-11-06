## Assignment 3 - Data Formats
#### Due: Thursday Sep 11th by classtime.

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
|------|----------------------------------------------|--------:|
| csv  |Comma seperated values                        | 484MB   |
| sql  |Structured Query Language (insert statements) | 467MB   | 
| xml  |EXtensible Markup Language                    | 2.3GB   |
| yaml |Yet Another Markup Language                   | 771MB   |
| json |Javascript Object Notation                    | ?       |

Each format has it's benefits, and detractors. Also, as you can see, we are missing the JSON file format. 

You will need one or more of the files to complete your assignment. To gain access to the files 
you can use the following link: 

http://cs.mwsu.edu/~griffin/5443-BigData

## Part One

- You should already have `/var/www/html/BigData` created.
- Create a folder in your `/var/www/html/BigData` directory called `FileFormats`
- Copy the files from http://cs.mwsu.edu/~griffin/5443-BigData to your folder.

How can this be done? Here's two ways (run them from the command line inside your folder):

- `curl -o GpsFilePoints.csv http://cs.mwsu.edu/~griffin/5443-BigData/GpsFilePoints.csv`
- `wget http://cs.mwsu.edu/~griffin/5443-BigData/GpsFilePoints.csv -O GpsFilePoints.csv`

- Repeat for each file. I'll show you how to write a script in class to automate it for all files.
- We will also discuss ways to speed this whole process up.
- When finished you should have a directory listing in `/var/www/html/BigData/FileFormats`  similar to the one above.

## Part Two

A little explanation of JSON.

### Json

Here is an example of a json object. It's stored in plain text (ascii or utf8):

```json
{
  "Lat": 33.847520500,
  "Lon": -98.567898800,
  "Time": 1249039453,
}
```
- The `{ }` define an "object".
- The `"Time" : 1249039453` is an example of a key value pair, which is the backbone of json.
- So an "object" is a set of "key value pairs" contained within curly braces.

What if you wanted an array of items?
- `[ ]` Square brackets define an array.
- `[1,2,3,4,5]` is an array of the values 1 through 5.

What if you wanted an array of objects?

Here is an array of two location objects:
```json
[
    {
      "Lat": 33.847520500,
      "Lon": -98.567898800,
      "Time": 1249039453,
    }
    ,
    {
      "Lat": 33.84752123440,
      "Lon": -98.567234898,
      "Time": 1249039455,
    }
]
```
You can combine `{}` (objects) `key:value` and `[ ]` arrays in an infinite number of possibilities allowing it to describe complex data. 

Here's an example of the top three sections of a sudoku board:)

```json
[
    [
     [3,9,1],
     [4,8,7],
     [6,5,2]
    ]
    ,
    [
     [2,8,6],
     [3,5,9],
     [7,1,4]
    ]
    ,
    [
     [5,7,4],
     [1,2,6],
     [8,3,9]
    ]
]

```

What if you weren't sure if your json is valid?

- You can go here: http://jsonlint.com/ and it will validate json for you.

### The conversion

- You should have `/var/www/html/BigData/FileFormats` created with your gps files in it.
- Place all of your scripting in here to complete the conversion from one of the files to Json. 
- Use any language you see fit, but since I'm post editing this document, python would be my choice :) Make sure you call it `conversion.??` and replace the `??` with your languages extension.
- I don't care how you get it done. You've seen plenty of examples in class by now.

### The write up

- Explain what language you used, and why, to convert one file to json. Did the language you chose effect which file you converted from?
- Now assume that you would be writing the code from scratch, in a language of your choice (without a library). This should effect your decision! So explain what language you would use, and which format you would choose to convert to json.
- When you do convert one of the files to json, what is the final file size?

### In Addition

- I'm also curious about how well each file compresses, so in your writeup, include which of the files compresses the best using zip and gzip. Include the original size and the compressed size and the percent compressed. 
- Which files had a better compression ratio?
- Can you speculate as to why?

- I want you to write up your findings for this entire project using `Markdown` and place them in a file called `writeup.md` here `/var/www/html/BigData/FileFormats/writeup.md`

___Minimum of 1.5 pages or close to 1000 words.___


### When your done

You should have a directory structure that looks like:

-----
- ![1] /var/www/html
	- ![1] BigData
	  - ![1] FileFormats
	    - ![13] conversion.py
	    - ![8] GpsFilePoints.csv
	    - ![10] GpsFilePoints.sql
	    - ![7]  GpsFilePoints.xml
	    - ![11] GpsFilePoints.yml
	    - ![12] GpsFilePoints.json
	    - ![9] writeup.md
	- ![9] README.md

In addition, you should have `conversion.??` in this folder (I put a conversion.py as an example).

-----

___Now push your changes to Github!___

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
