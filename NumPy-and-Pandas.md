# NumPy
## Introduction
NumPy (Numerical Python) is a fundamental package for scientific computing in Python.
It provides support for arrays, matrices, and many mathematical functions.

### Key Features:

- Efficient array operations.
- Broadcasting.
- Linear algebra, Fourier transform, and random number capabilities.

## Basic Concepts
### 1] Array:

- A grid of values, all of the same type.
- Created using numpy.array().

```python
import numpy as np
arr = np.array([1, 2, 3])
```
### 2] Dimensions:

- 0-D: Scalar.
- 1-D: Vector.
- 2-D: Matrix.
- 3-D and higher: Tensor.

### 3] Attributes:

- ndarray.shape: Dimensions of the array.
- ndarray.dtype: Data type of elements.
- ndarray.size: Total number of elements.
- ndarray.ndim: Number of dimensions.

### 4] Array Creation:

- np.zeros(shape): Array filled with zeros.
- np.ones(shape): Array filled with ones.
- np.arange(start, stop, step): Array with evenly spaced values.
- np.linspace(start, stop, num): Array with specified number of elements.

### 5] Array Operations:

- Arithmetic Operations: +, -, *, /, **.
- Dot Product: np.dot(a, b).
- Reshape: arr.reshape(shape).
- Transpose: arr.T.

### 6] Indexing and Slicing:

- Similar to Python lists.
- Boolean Indexing: Filter elements based on conditions.

```python
arr[arr > 2]
```

### 7] Broadcasting:

- Allows arithmetic operations on arrays of different shapes.

### 8] Universal Functions (ufunc):

- Functions that operate on ndarrays in an element-by-element fashion.
- Examples: np.sin(), np.exp(), np.sqrt().

### 9] Linear Algebra:

- np.linalg.inv(): Inverse of a matrix.
- np.linalg.det(): Determinant of a matrix.
- np.linalg.eig(): Eigenvalues and eigenvectors.

### 10] Random Module:

- np.random.rand(): Random values in a given shape.
- np.random.randint(): Random integers.
- np.random.normal(): Normal distribution.




# Pandas

## Introduction
Pandas is a powerful data manipulation library in Python.
It provides data structures like Series and DataFrame.

### Key Features:

- Handling missing data.
- Data alignment and integrated handling.
- Group by functionality.
- Time series functionality.

## Basic Concepts
### 1] Series:

- One-dimensional array-like object.
- Can hold any data type.

```python
import pandas as pd
s = pd.Series([1, 2, 3])
```

### 2] DataFrame:

- Two-dimensional, size-mutable, and potentially heterogeneous tabular data.
- Created using pd.DataFrame().

```python

df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': ['a', 'b', 'c']
})
```

### 3] Attributes:

- df.shape: Dimensions of the DataFrame.
- df.columns: Column labels.
- df.index: Row labels.
- df.dtypes: Data types of columns.

### 4] DataFrame Creation:

From dictionary, list of dictionaries, CSV, Excel, etc.

```python

df = pd.read_csv('file.csv')
```

### 5] Data Selection:

1] Column Selection: df['column_name'].
2] Row Selection: df.loc[index], df.iloc[index].

Conditional Selection:

```python

df[df['A'] > 1]
```

### 6] Data Manipulation:

- Adding Columns: df['new_column'] = values.
- Dropping Columns: df.drop('column_name', axis=1).
- Renaming Columns: df.rename(columns={'old_name': 'new_name'}).
- Sorting: df.sort_values(by='column_name').

### 7] Handling Missing Data:

- Detect Missing Data: df.isnull().
- Drop Missing Data: df.dropna().
- Fill Missing Data: df.fillna(value).

### 8] Group By:

Split-apply-combine strategy.

```python

df.groupby('column_name').mean()
```

### 9] Merging and Joining:

- Concatenation: pd.concat([df1, df2]).
- Merge: pd.merge(df1, df2, on='key').

### 10] Pivot Tables:

- Create a spreadsheet-style pivot table.

```python

df.pivot_table(values='D', index=['A', 'B'], columns=['C'])
```

### 11] Time Series:

- Date Range: pd.date_range(start, periods).
- Resampling: df.resample('D').mean().

### 12] Input/Output:

- Reading: pd.read_csv(), pd.read_excel().
- Writing: df.to_csv(), df.to_excel().

## Integration of NumPy and Pandas
- NumPy arrays can be converted to Pandas DataFrame and vice versa.

```python

df = pd.DataFrame(np.random.rand(3, 3))
arr = df.to_numpy()
```


# SQLAlchemy
SQLAlchemy is divided into two main components:

- Core: A SQL abstraction toolkit that allows direct interaction with databases using Python.
- ORM: An Object-Relational Mapper that allows Python classes to be mapped to database tables, enabling object-oriented database interactions.


## Key Concepts and Components
### 1] create_engine
- The create_engine function is used to create a database connection.
- It takes a database URL as an argument (e.g., sqlite:///data for SQLite).
- The echo=True parameter enables logging of SQL statements executed by SQLAlchemy.

```python

from sqlalchemy import create_engine
engine = create_engine('sqlite:///data', echo=True)
```

### 2] MetaData
- MetaData is a container object that keeps track of tables and their schemas.
- It is used to define and manage database tables.

```python

from sqlalchemy import MetaData
metadata = MetaData()
```

### 3] Table and Column
- Table is used to define a database table.
- Column is used to define the columns of a table, including their data types and constraints.

```python

from sqlalchemy import Table, Column, Integer, String, ForeignKey

users = Table('users', metadata,
    Column('id', Integer, primary_key=True),
    Column('name', String),
    Column('age', Integer),
    Column('city', String),
)

posts = Table('posts', metadata,
    Column('id', Integer, primary_key=True),
    Column('title', String),
    Column('content', String),
    Column('user_id', Integer, ForeignKey('users.id')),
)
```
- Primary Key: The primary_key=True parameter marks a column as the primary key.
- Foreign Key: The ForeignKey('users.id') parameter establishes a relationship between the posts table and the users table.

### Creating Tables
The metadata.create_all(engine) method creates all the tables defined in the metadata object in the database.

```python

metadata.create_all(engine)
```
### Inserting Data
- The insert function is used to create an INSERT statement.
- The values method specifies the data to be inserted.

```python

from sqlalchemy import insert

with engine.connect() as con:
    # Insert into 'users' table
    insert_stmt = insert(users).values(name='John', age=20, city='New York')
    result = con.execute(insert_stmt)
    print(result.rowcount)  # Number of rows affected

    # Insert into 'posts' table
    insert_stmt = insert(posts).values(title='Post 1', content='Content 1', user_id=1)
    result = con.execute(insert_stmt)
    print(result.rowcount)  # Number of rows affected

    # Commit the transaction
    con.commit()
```

### Querying Data
- The select function is used to create a SELECT statement.
- The execute method runs the query, and the result can be iterated over to access rows.

```python

from sqlalchemy import select

with engine.connect() as con:
    # Select all rows from 'users' table
    select_stmt = select(users)
    result = con.execute(select_stmt)
    for row in result:
        print(row)  # Each row is a tuple

    # Select all rows from 'posts' table
    select_stmt = select(posts)
    result = con.execute(select_stmt)
    for row in result:
        print(row)  # Each row is a tuple
```

### Database Transactions
- SQLAlchemy automatically manages transactions when using the engine.connect() context manager.
- Changes are committed using con.commit().
- If an error occurs, the transaction can be rolled back using con.rollback().
