## Processing a file with Redis

Using Python + Redis, acquire the following information from `nutrition.json`

#### Preliminaries

- Create a folder on your server called `Assignment6` in `/var/www/html`.
- Copy `nutrition.json` into this folder.
- For each of the following questions, create a file called Problem_x.py, replacing the `x` with the problem number.
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

- This problem is more about size of the database depending on how data is stored. So I will give you instructions for storing the data in two ways. I want the size of the data base on disk (remember info && human readable). You will also need to make sure you run `flushall` before each loading.




