# Spark-RDD-Cheat-Sheet

According to the seminal paper on Spark, RDDs are immutable, fault-tolerant, parallel data structures that let users explicitly persist intermediate results in memory, control their partitioning to optimize data placement, and manipulate them using a rich set of operators.

## RDD Operations

The RDD operations are classified into two types: Transformations and Actions. Transformation operations are lazily evaluated, meaning Spark will delay the evaluations of the invoked operations until an action is taken.

### Creating RDDs

- The first way to create an RDD is to parallelize an object collection, meaning
converting it to a distributed dataset that can be operated in parallel.
The way to parallelize an object collection is to call the parallelize method of the
SparkContext class.
```
val stringList = Array("Spark is awesome","Spark is cool")
val stringRDD = spark.sparkContext.parallelize(stringList)
```
- The second way to create an RDD is to read a dataset from a storage system, which
can be a local computer file system, HDFS, Cassandra, Amazon S3, and so on.
```
val fileRDD = spark.sparkContext.textFile("/tmp/data.txt")
```
