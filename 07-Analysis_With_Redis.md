## Processing a file with Redis

Due Thursday 7 October.

#### Overview

Using Python + Redis, load selected data from `nutrition_clean.json` into our Redis key/store.

#### Preliminaries

- In the folder on your server at `/var/www/html/BigData/Redis`, create a sub folder called `Solutions`.
- Use the `nutrition_clean.json` in this folder to process.
- For each of the following questions, create a file called `Problem_x.py`, replacing the `x` with the problem number.
- I should be able to run each program without error. Each program might not have output necessarily, but it should still run.

#### Little Help

As a help to you, I created this small subset of the nutrients file [here](http://cs.mwsu.edu/~griffin/redis/xaa) to make it visually digestible. The trick is to have an extension installed in your browser to format the json! I have [this](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc) chrome extension installed to help me view large json files.

### Problems

##### 1)

- What are the number of unique food "items" in the file. You might be tempted to count the number of lines, since we assume that each line contains one food item. I will warn you that this is an incorrect solution. Just by chance, there might be a few duplicated rows in the file, therefore line counting would be wrong.

>Output:
>
>Unique items: xxxxx

##### 2)

- How many unique nutrients are there?

>Output:
>
>Unique nutrients: _xxxxx_

##### 3)
- What are the top 5 most commonly occuring nutrient?

>Output:
>
> - 1 _____________ occurs _xxx_ number of times.
> - 2 _____________ occurs _xxx_ number of times.
> - ...
> - 5 _____________ occurs _xxx_ number of times.


##### 4)
- Given a specific nutrient, what percentage of food items contain this nutrient?

>Output:
>
> __________ occurs in _x_% number if food items.


#### 5)

- This problem is more about size of the database depending on how data is stored. I want the size of the data base on disk (remember info && human readable). You will also need to make sure you run `flushall` before loading this structure.You can make multiple passes on the data, and I'm not looking for extremely efficient processing, I just want it loaded as prescribed. You don't have to perform tasks in the order asked either. I just want to final resulting data structures, and size of all of them on disk.

- Store all id's for nutrients in a set.
- Store all nutrients in a hash with thier id's as keys.
- Store all tagnames in a set.
- Store all nutrients in a hash with tagnames as keys.
- Store all nutrient id's in a list with the item id (top level _id) as the key.


### Writeup

- Create a file called `writeup.md` in your `Solutions` folder.
- Write an organized document (using markdown) listing all your solutions, and small descriptions on how you solved them.
- For example:

> 1)What are the number of unique food "items" in the file. You might be tempted to count the number of lines, since we assume that each line contains one food item. I will warn you that this is an incorrect solution. Just by chance, there might be a few duplicated rows in the file, therefore line counting would be wrong.

> Output:
>
> Unique items: xxxxx

> In my solution I opted to use a redis "hash" since all keys must be unique. I used the "_id" field as the "key" and the description as the "value", (e.g. `HSET key value`). I could then use `HLEN` to count the number of unique id's in the hash, thereby giving me the number of unique values in the data set.

__After your done, you should have a directory structure similar to:__

-----

- ![1] /var/www/html
	- ![1] BigData
	  - ![1] FileFormats
	  - ![1] Hadoop
	  - ![1] Redis
	      - ![1] Solutions
	          - ![13] Problem_1.py
	          - ![13] Problem_2.py
	          - ![13] Problem_3.py
	          - ![13] Problem_4.py
	          - ![13] Problem_5.py
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


