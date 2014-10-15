### Assignment 3 - Installing Hadoop.
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
- Add a file called WriteUp.md to this folder (this will contain answers to the next section).


#### Write Up

- How do you add nodes to your Hadoop cluster?
- Can everyone in class add the remaining members of the class to thier cluster? This asks the question: "Can everyone simultaneously run thier own Hadoop cluster, AND be a slave (worker) in another Hadoop cluster?" This would obviously never be ideal in the real world, but can this work as a model in our BigData course? Otherwise, you will be running your assignments on a single server, which doesn't fit with the whole `Big Data` theme.


Write your answer up in a file named: `Assignment3-Writeup.md` and put it in your repository. 
