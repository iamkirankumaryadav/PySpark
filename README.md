# PySpark

### Import library
```python
from pyspark.sql import SparkSession
import pandas as pd
```

### Create a variable for starting a session
```python
# Set environment variables:
import os
import sys

os.environ['PYSPARK_PYTHON'] = sys.executable
os.environ['PYSPARK_DRIVER_PYTHON'] = sys.executable

# PySpark applications start with initializing SparkSession:
spark = SparkSession.builder.appName("spark").getOrCreate()
spark.conf.set("spark.sql.execution.arrow.enabled", "true")
spark
```

```terminal
# Output
SparkSession - in-memory
SparkContext

Spark UI
Version   v3.4.1
Master    local[*]
AppName   spark
```

### Read a dataset and create a dataframe
```python
# Read the file: 
df = spark.read.csv('Data.csv', header=True, inferSchema=True)

# Show the dataframe:
df.show()

# Show the schema details:
df.printSchema()
```
```output
# df.show():
+-----------+----+------------------------+
|       Name| Age|             Designation|
+-----------+----+------------------------+
| Kirankumar|  28| Data Science Specialist|
|  Paramveer|  29|            Data Analyst|
|     Gaurav|  29|                     SDE|
+-----------+----+------------------------+

# df.printSchema():
root
  | -- Name: string (nullable = true)
  | -- Age: integer (nullable = true)
  | -- Role: string (nullable = true)
```

### Data type of a variable

```python
# Data type:
type(df)
```

```output
pyspark.sql.dataframe.DataFrame
```

### Get the column names
```python
# List of all the column names:
df.columns
```

### Select top 3 rows
```python
# Show only top n rows:
df.head(3)
# In pyspark, the output will be a list not a dataframe.
```
```terminal
# Output:
[Row(Name='Kirankumar', Age=28, Role='Data Science Speicalist'),
 Row(Name='Paramveer', Age=29, Role='Data Analyst'),
 Row(Name='Gaurav', Age=29, Role='SDE')]
```

### Show specific column
```python
# Select a particular column:
df.select('Name').show()
```

### Show multiple columns
```python
# Pass list of columns to display multiple columns:
df.select(['Name', 'Experience']).show()
```

**PySpark DataFrame** can be created by passing a list of `lists`, `tuples`, `dictionaries`, `pyspark.sql.Rows` (List of Rows), a `pandas DataFrame` and an `RDD` list.

## Create DataFrame using Pandas

```python
import pandas as pd
data = {
    'Name': ['Kirankumar Yadav', 'Suraj Sanka', 'Sumit Suman'],
    'Age': [28, 28, 27],
    'Designation': ['Data Science Specialist', 'DevOps Engineer', 'Python Developer']
}

df = pd.DataFrame(data)
df
```

Name|Age|Designation
:---|:---|:---
Kirankumar Yadav|28|Data Science Specialist
Suraj Sanka|28|DevOps Engineer
Sumit Suman|27|Python Developer

```python
# Create spark DataFrame from Pandas DataFrame:
sdf = spark.createDataFrame(df)
sdf.show()
```

```output
# Show all the columns
+-----------------+----+------------------------+
|             Name| Age|             Designation|
+-----------------+----+------------------------+
| Kirankumar Yadav|  28| Data Science Specialist|
|      Suraj Sanka|  28|         DevOps Engineer|
|      Sumit Suman|  27|        Python Developer|
+-----------------+----+------------------------+
```

### Converting the spark DataFrame to Pandas DataFrame 

```python
sdf.toPandas().head()
```

Name|Age|Designation
:---|:---|:---
Kirankumar Yadav|28|Data Science Specialist
Suraj Sanka|28|DevOps Engineer
Sumit Suman|27|Python Developer

### Description of Data Frame (Especially numerical features)

```python
# Statistical descriptions (count, mean, stddev, max, min):
sdf.describe().show()
```

### Define the schema of a DataFrame

```python
from pyspark.sql.types import StructField, StringType, IntegerType, StructType

# Define schema:
data_schema = [StructField(name='age', dataType=IntegerType(), nullabel=True), StructField(name='name', dataType=StringType(), nullable=True)]
new_schema = StructType(fields=data_schema)

sdf = spark.read.json('People.json', schema=new_schema)
sdf.printSchema()
```

### Create/Add a new column

```python
sdf.withColumn(colName='New Age', col=sdf['age']).show()
sdf.withColumn(colName='New Age', col=sdf['age'] * 2).show()
```


### Rename the existing column

```python
sdf.withColumnRenamed(existing='sex', new='gender').show()
```

### Create a temporary view like SQL view

```python
sdf.createOrReplaceTempView('People')

# We can write SQL queries to select the data:
spark.sql('SELECT * FROM people WHERE age > 20').show()
```
