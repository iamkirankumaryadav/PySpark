# PySpark Code Snippets:

### Create a dataframe using dictionaries
```python
# Import Libraries:
import os
import pandas as pd
from pyspark.sql import SparkSession, DataFrame
from pyspark.sql.types import StructType, StructField, IntegerType, StringType
import sys

# Set environment variables:
os.environ['PYSPARK_PYTHON'] = sys.executable
os.environ['PYSPARK_DRIVER_PYTHON'] = sys.executable

# Create a spark session:
spark = SparkSession.builder.appName("spark").getOrCreate()
spark.conf.set("spark.sql.execution.arrow.enabled", "true")

# Create data:
data = {
    'Name': ['Kirankumar', 'Suraj', 'Sumit', 'Nilay', 'Karthik'],
    'Age': [28, 28, 26, 26, 32],
    'Designation':['Data Scientist', 'DevOps', 'Python Developer', 'QA Analyst', 'Business Consultant']
}

# Create a dataframe from dictionary:
df = pd.DataFrame(data)

# Create schema:
schema = StructType([
    StructField(name='Name', dataType=StringType(), nullable=True), 
    StructField(name='Age', dataType=IntegerType(), nullable=True),
    StructField(name='Designation', dataType=StringType(), nullable=True)
])

# Create a dataframe using spark:
df = spark.createDataFrame(data=df, schema=schema)

# Show dataframe:
df.show()

# Print schema:
df.printSchema()
```    

### Create dataframe from list of tuples

```python
# Import Libraries:
import os
from pyspark.sql import SparkSession, DataFrame
from pyspark.sql.types import StructType, StructField, IntegerType, StringType
import sys

# Set environment variables:
os.environ['PYSPARK_PYTHON'] = sys.executable
os.environ['PYSPARK_DRIVER_PYTHON'] = sys.executable

# Create a spark session:
spark = SparkSession.builder.appName("spark").getOrCreate()
spark.conf.set("spark.sql.execution.arrow.enabled", "true")

# Create list of tuples:
data = [
    ('Kirankumar', 28, 'Data Scientist'), 
    ('Suraj', 28, 'DevOps Engineer'),
    ('Sumit', 26, 'Python Developer'),
    ('Nilay', 26, 'QA Analyst'), 
    ('Karthik', 32, 'Business Consultant')
]

# Create schema:
from pyspark.sql.types import StructType, StructField, IntegerType, StringType
schema = StructType([
    StructField(name='Name', dataType=StringType(), nullable=True), 
    StructField(name='Age', dataType=IntegerType(), nullable=True),
    StructField(name='Designation', dataType=StringType(), nullable=True)
])

# Create dataframe:
df = spark.createDataFrame(data=data, schema=schema)

# Show dataframe:
df.show()

# Print schema:
df.printSchema()
```
