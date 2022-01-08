# Spark-RDD-Cheat-Sheet
Spark RDD Cheat Sheet

val spark = SparkSession
  .builder()
  .appName("Spark SQL basic example")
  .master("local")
  .getOrCreate()
