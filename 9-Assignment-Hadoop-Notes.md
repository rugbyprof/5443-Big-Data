## Hadoop Assignment Notes

### Hadoop Cluster Setup

http://dogdogfish.com/2014/04/26/installing-hadoop-2-4-on-ubuntu-14-04/

### Make Hadoop is Running

I'm not sure how this will effect a multi user setting, but:

___Start Hadoop___
```
/usr/local/hadoop/sbin/start-dfs.sh && /usr/local/hadoop/sbin/start-yarn.sh
```

___Change to your Hadoop directory___

```bash
cd /usr/local/hadoop/users/yourusername
wget -O 'count_of_monte_cristo.txt' http://www.gutenberg.org/cache/epub/1184/pg1184.txt
```

___Add to hadoop file system___

- Create a folder in hadoop fs
- Put a file in the folder simultaneously adding to hadoop fs

```bash
/usr/local/hadoop/bin/hadoop fs -mkdir /usr/local/hadoop/users/yourusername/input
/usr/local/hadoop/bin/hadoop fs -put /usr/local/hadoop/users/yourusername/count_of_monte_cristo.txt /input
```

Has it worked?

Run this command from `/usr/local/hadoop/users/yourusername`:

```
/usr/local/hadoop/bin/hadoop fs -ls /input
```

### The Mapper

```python
#!/usr/bin/python
 
import sys
 
for line in sys.stdin:
    for word in line.strip().split():
        print "%s\t%d" % (word, 1)
```

- Save your file in /usr/local/hadoop/users/yourusername/word_mapper.py.
- Also, make sure it’s executable: `chmod +x word_mapper.py`

__Has it worked?__
Run this command: 
```
/usr/local/hadoop/bin/hadoop fs -cat /input/count_of_monte_cristo.txt | /home/hduser/word_mapper.py
```

### The Reducer

We’ve got ourselves a nice stream of words. The Hadoop streaming jar will take care of the sorting for us (though we can override the default behaviour should we choose) so we just need to decide what to do with that stream of words. I’m going to propose this:

```python
#!/usr/bin/python
 
import sys
 
current_word = None
current_count = 1
 
for line in sys.stdin:
    word, count = line.strip().split('\t')
    if current_word:
        if word == current_word:
            current_count += int(count)
        else:
            print "%s\t%d" % (current_word, current_count)
            current_count = 1
 
    current_word = word
 
if current_count > 1:
    print "%s\t%d" % (current_word, current_count)
```

- Follow the code through and try to think of the different cases it's trying to catch. 
- The first and last lines are tricky but play around with it – what happens if I just feed a file containing one word? 
- What about a file with no duplicate words? 
- Think about all the different cases and hopefully – the above code handles them all as you’d expect. 


__Has it worked?__

Make sure that file is executable: `chmod +x /home/hduser/word_reducer.py`

Run this:

```
/usr/local/hadoop/bin/hadoop fs -cat /input/count_of_monte_cristo.txt | /home/hduser/word_mapper.py | head -n 100 | sort | /home/hduser/word_reducer.py
```

If everything’s gone to plan you should see a bunch of lines and associated counts – some of them should be non-one's.


___Run the Mapreduce___

This is what you’ve been waiting for. Well – it’s what I’ve been waiting for at least. Run this command and you’ll basically be a Hadoop hero:

```
cd /usr/local/hadoop
bin/hadoop jar share/hadoop/tools/lib/hadoop-streaming-2.4.0.jar -files /home/hduser/word_mapper.py,/home/hduser/word_reducer.py -mapper /home/hduser/word_mapper.py -reducer /home/hduser/word_reducer.py -input /input/count_of_monte_cristo.txt -output /output
```

And off it goes – enjoy watching your mapreduce race through at what I’m sure is a barely tolerable crawl.

__Has it worked?__
Run this command:

```
/usr/local/hadoop/bin/hadoop fs -cat /output/part-00000
```

If you see a stream of likely looking results – you’re golden. If you want to get the file out of HDFS for inspection run something like this:

```
/usr/local/hadoop/bin/hadoop fs -get /output/part-00000 /home/hduser/monte_cristo_counted.txt
less /home/hduser/monte_cristo_counted.txt
```

Source: http://dogdogfish.com/2014/05/19/hadoop-wordcount-in-python/
