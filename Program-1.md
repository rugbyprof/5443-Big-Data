## Program 1 - Getting Our Feet Wet
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

- Create a fodler in your `/var/www/html` directory called `BigData`
- Create a folder in your `/var/www/html/BigData` directory called `GpsData`
- Copy the files from http://cs.mwsu.edu/~griffin/5443-BigData to your folder.

How can this be done? Here's two ways (run them from the command line inside your folder):

- `curl -o GpsFilePoints.csv http://cs.mwsu.edu/~griffin/5443-BigData/GpsFilePoints.csv`
- `wget http://cs.mwsu.edu/~griffin/5443-BigData/GpsFilePoints.csv -O GpsFilePoints.csv`

- Repeat for each file. I'll show you how to write a script in class to automate it for all files.
- We will also discuss ways to speed this whole process up.
- When finished you should have a directory listing in `/var/www/html/BigData/GpsData`  similar to the one above.

## Part Two

- What would you do to convert any of the above files into a `json` representation? You do not have to write the code or find a library to do this, but I want you to explain your approach.
- Even though you do not have to implement this, I want you to assume that you would have to write the code from scratch. So, based on this fact, which format would you choose to convert from?

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

### ~~The conversion~~

- Create a folder in your `/var/www/html/BigData` folder called `Program1`
- Place all of your scripting in here to complete the conversion.
- I don't care how you get it done. First, I started giving an example to help with the solution, but now I'm more interested in your process than the solution. So ... no help.

### The write up

I want to know:
- What language you choose, to do your conversion and why.
- What file you choose to convert from, and why.
- ~~I want to know the size of the completed json.~~

I also want to know:
- I want to know which of the files compresses the best using zip and gzip.
- I want you to write up your findings for this entire project using `Markdown` and place them in a file called `Program1-Writeup.md`




 

 
