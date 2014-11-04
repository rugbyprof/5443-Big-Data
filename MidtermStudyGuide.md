## Midterm Study Guide

### Chapter 1

Define:

- ___Distributed computing___
- ___Sharding___
- ___Data Silo___

Which database back-end should be used: relational, key–value, or something else? 


What is the "Ultimate Database"?

Four Rules of Success:
    - Build Solutions That Scale
    - Build Systems That Can Share Data
    - Build Solutions Not Infrastructure
    - Focus on Unlocking Value from Your Data
 
--

### Chapter 2

Describe the challenges of sharing lots of files.
    - Choosing How to Store the Data
    - Choosing the Right Data Format
    - How to Present the Data

Describe ___Infrastructure as a service___ (IAAS).

Many companies choose to store data in the cloud to alleviate problems with managing their own infrastructure (security, backups, etc.). Describe why the cloud may or may not necessarily be the answer to storing "big data".

- File Formats
    - Json
    - Csv
    - Xml
    - Yaml

Define ___data serialization___.

--

### Chapter 3

What is ___ACID___?

Briefly describe the difference between the `relational` and `key value` database models. Give pros and cons for each as they apply to scalability.

When storing a dataset across multiple server instances, a ___sharding strategy___ needs to be chosen. Describe what this means, and give examples.

The ___Ketema algorithm___ is a hashing algorithm that provides a strategy known as ___consistent hashing___. Explain in detail what `consistent hashing` is, how the `Ketema algorithm` works, and what they can be applied to.

What is a major hindrance when querying ___key value stores___? Compare this to querying a typical SQL database.  

