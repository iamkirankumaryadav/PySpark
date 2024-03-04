# **DataFrame Operations**

### Creata a Spark Session

```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName('operations').getOrCreate()
sdf = spark.read.csv('Data.csv', inferSchema=True, header=True)
sdf.printSchema()
sdf.show()
```

### Apply filters

```python
sdf.filter('Close < 200').select(['Date', 'Open', 'Close', 'High', 'Low']).show()

sdf.filter(sdf['Close'] < 200).select(['Date', 'Open', 'Close', 'High', 'Low']).show()

# Using & / | operators:
sdf.filter((sdf['Close'] < 200) & (sdf['Open'] > 200)).select(['Open', 'High', 'Low', 'Close']).show(5)
```

### Group by an aggregate

```python
# Aggregate functions: sum(), mean(), count(), max(), and min()[
sales.groupby('Company').mean().show()

# Aggregate muliple columns:
sales.groupby('Company').agg({'Sales': 'sum', 'Person': 'max'}).show()
```

### Aggrgate functions

```python
from pyspark.sql.functions import countDistinct, avg, stddev, format_number

sales.select(countDistinct(col='Sales')).show()
sales.select(avg(col='Sales').alias('Average Sales')).show()
sales.select(stddev(col='Sales')).show()
sales.select(format_number(stddev(col='Sales'), 2).alias('Standard Deviation')).show()
```

### Order by values

```python
# Ascending order:
sales.orderBy('Sales').show()

# Descending order:
sales.orderBy(sales['Sales'].desc()).show()
```

### Handle missing value

```python
# Drop:
data.na.drop().show()

# Set threshold i.e. Drop if the value if its missing more than 2 times:
data.na.drop(thresh=2).show()

# All the row values should have NULL:
data.na.drop(how='all').show()

# Consider only particular column:
data.na.drop(subset='Sales').show()

# Fill missing value:
data.na.fill(value='No Name', subset='Name').show() # String
data.na.fill(value=0, subset='Sales').show() # Numeric/Integer

# Fill missing value with mean of a column:
average = data.select(mean(col=data['Sales'])).collect()
mean_value = average[0][0]
data.na.fill(value=mean_value, subset='Sales').show()
```      
