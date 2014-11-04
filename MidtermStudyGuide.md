## Midterm Study Guide

Define:

- ___Big Data___
- ___Distributed computing___
- ___Sharding___
- ___Data Silo___
- ___Data Wharehouse___
- ___Data Serialization___

--

Describe the challenges of sharing lots of files. Discuss formats, transferring over networks, size, etc.

Describe ___Infrastructure as a service___ (IAAS). Many companies choose to store data in the cloud to alleviate problems with managing their own infrastructure (security, backups, etc.). Describe why the cloud may or may not necessarily be the answer to storing "big data". Give examples of problems that IAAS would alleviate for a company, as well as some problems it may cause.

- File Formats
    - Json
    - Csv
    - Xml
    - Yaml

In general, have a good understanding of each file format, and what it may or may not be good for. 

--

What is ___ACID___?

Briefly describe the difference between the `relational` and `key value` database models. Give pros and cons for each as they apply to scalability.

When storing a dataset across multiple server instances, a ___sharding strategy___ needs to be chosen. Describe what this means, and give examples.

The ___Ketema algorithm___ is a hashing algorithm that provides a strategy known as ___consistent hashing___. Explain in detail what `consistent hashing` is, how the `Ketema algorithm` works, and what they can be applied to.

What is a major hindrance when querying ___key value stores___? Compare this to querying a typical SQL database.  

What is the "Ultimate Database"?
