## Midterm Study Guide
#### November 11<sup>th</sup> at 5:30 p.m.

### Part 1
Define:

1.  ___Big Data___
- ___Distributed computing___
- ___Sharding___
- ___Data Silo___
- ___Data Wharehouse___
- ___Data Serialization___

### Part 2
1. Describe the challenges of sharing lots of files. Discuss formats, transferring over networks, size, etc.

8. Describe ___Infrastructure as a service___ (IAAS). Many companies choose to store data in the cloud to alleviate problems with managing their own infrastructure (security, backups, etc.). Describe why the cloud may or may not necessarily be the answer to storing "big data". Give examples of problems that IAAS would alleviate for a company, as well as some problems it may cause.

9. File Formats (In general, have a good understanding of each file format, and what it may or may not be good for. )
    - Json
    - Csv
    - Xml
    - Yaml
10. What is ___ACID___?

11. Briefly describe the difference between the `relational` and `key value` database models. Give pros and cons for each as they apply to scalability.

12. When storing a dataset across multiple server instances, a ___sharding strategy___ needs to be chosen. Describe what this means, and give examples.

13. The ___Ketama algorithm___ is a hashing algorithm that provides a strategy known as ___consistent hashing___. Explain in detail what `consistent hashing` is, how the `Ketama algorithm` works, and what they can be applied to.

14. What is a major hindrance when querying ___key value stores___? Compare this to querying a typical SQL database.  

15. What would be the "Ultimate Database"?

### Part 2

16. Describe Hadoop (HDFS,MapReduce).

17. Discuss any problems that may arise by not employing a secondary namenode?

18. Describe why files have to be moved/ingested into HDFS before they can be processed.

19. Lets assume that the default block size is 64 Mb and the replication factor is 3. Explain why Hadoop 
has such a large block size (regular file systems use 1k or so) and what the replication factor means.
