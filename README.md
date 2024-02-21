# PySpark

### Import library
```python
from pyspark.sql import SparkSession
```

### Create a variable for starting a session
```python
spark = SparkSession.builder.appName('Dataframe').getOrCreate()
spark
```

```terminal
# Output
SparkSession - in-memory
SparkContext

Spark UI
Version v3.1.1
Master local[*]
AppName Dataframe
```

### Read a dataset and create a dataframe
```python
df = spark.read.csv('file.csv', header=True, inferSchema=True)
```

### Display the dataframe
```python
df.show()
```

### Check the schema
```python
df.printSchema()
```

```terminal
# Output:
root
  | -- Name: string (nullable = true)
  | -- Age: integer (nullable = true)
  | -- Role: string (nullable = true)
```

### Data type of a variable

```python
type(df)
```

```output
pyspark.sql.dataframe.DataFrame
```

### Get the column names
```python
df.columns
```

### Select top 3 rows
```python
df.head(3)

# In pyspark, the output will be a list not a dataframe.
```
```terminal
# Output:

[Row(Name='Kirankumar', Age=28, Role='Data Science Speicalist'),
 Row(Name='Paramveer', Age=29, Role='Data Analyst'),
 Row(Name='Gaurav', Age=29, Role='SDE')]
```
