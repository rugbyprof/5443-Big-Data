### Assignment 4 - Installing Hadoop.
#### Due: Tue Sep 16<sup>th</sup> by class time.

#### Install Hadoop
-----

Follow the steps in the tutorial [here](https://www.digitalocean.com/community/tutorials/how-to-install-hadoop-on-ubuntu-13-10), to install hadoop on your server.

-----

- When your done, do a `whereis hadoop`, it should give you a location.
- Remember to start your server you run: `start-dfs.sh` (answer the prompts)
- Also enter: `start-yarn.sh`
- Then finally run `jps` from the command line. You should get something "similar" but not exactly like:

![](http://f.cl.ly/items/2y1Q2T0U2P3i0K0E2Z0i/jps.png)

- Take a screen shot to put in your write up.

#### Where to place your write up

- Create a folder called `Hadoop` in `/var/www/html/BigData`
- Add a file called `writeup.md` to this folder (this will contain answers to the next section).
- Your new file structure should look like:

-----

- ![1] /var/www/html
	- ![1] BigData
	  - ![1] FileFormats
	  - ![1] Hadoop
	    - ![9] writeup.md
	- ![9] README.md
	
-----


#### Write Up

___Answer the following questions, and place them in your `writeup.md` file.___

1. How do you add nodes to your Hadoop cluster?
2. Can everyone in class add the remaining members of the class to thier cluster? This asks the question: "Can everyone simultaneously run thier own Hadoop cluster, AND be a slave (worker) in another Hadoop cluster?" This would obviously never be ideal in the real world, but can this work as a model in our BigData course? Otherwise, you will be running your assignments on a single server, which doesn't fit with the whole `Big Data` theme.
3. Our digital ocean servers only have 512MB of Ram. Can you speculate WHY Hadoop cannot run on a server with such minimal resources? Here are some areas to think about:
    - Large amount of object code needing to reside in memory?
    - Large amount of threads hogging resources?
    - The Hadoop file system requires a lot of memory? (Not disk space, but ram).

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
