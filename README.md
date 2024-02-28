# PySpark

### Import library
```python
from pyspark.sql import SparkSession
```

### Create a variable for starting a session
```python
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
df = spark.read.csv('Data.csv', header=True, inferSchema=True)
```

### Display the dataframe
```python
df.show()
```
```output
# Show all the columns
+-----------+----+------------------------+
|       Name| Age|             Designation|
+-----------+----+------------------------+
| Kirankumar|  28| Data Science Specialist|
|  Paramveer|  29|            Data Analyst|
|     Gaurav|  29|                     SDE|
+-----------+----+------------------------+
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

### Show specific column
```python
df.select('Name').show()
```

### Show multiple columns
```python
df.select(['Name', 'Experience']).show()
```

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

|Name|Age|Designation
---|---|---|---
0	|Kirankumar Yadav|28|Data Science Specialist
1	|Suraj Sanka|28|DevOps Engineer
2	|Sumit Suman|27|Python Developer


```python
# Create spark DataFrame from Pandas DataFrame
sdf = spark.createDataFrame(df)
sdf.show()
```
