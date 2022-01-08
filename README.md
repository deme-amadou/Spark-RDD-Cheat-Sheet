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
-The third way to create an RDD is by invoking one of the transformation operations
on an existing RDD.

### Transformations

#### map(func)
The most fundamental, versatile, and commonly used transformation is the map operation. It is used to transform some aspect of the data per row to something else.

- Using a Map Transformation to Convert All Characters in the String to Uppercase
```
val allCapsRDD = stringRDD.map(line => line.toUpperCase)
allCapsRDD.collect().foreach(println)
```
- Defining a Function and Using It in the Map Transformation
```
def toUpperCase(line:String) : String = {  line.toUpperCase }
stringRDD.map(l => toUpperCase(l)).collect.foreach(println)
```
- Using a map Transformation to Convert Text Data into Scala Contact
Objects
```
case class Contact(id:Long, name:String, email:String)
val contactData = Array("1#John Doe#jdoe@domain.com","2#Mary
Jane#mjane@domain.com")
val contactDataRDD = spark.sparkContext.parallelize(contactData)
val contactRDD = contactDataRDD.map(l => {
         val contactArray = l.split("#")
         Contact(contactArray(0).toLong, contactArray(1), contactArray(2))
})
contactRDD.collect.foreach(println)
```
