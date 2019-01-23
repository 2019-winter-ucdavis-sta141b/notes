# Translating Between R and Python

## Things That Are The Same

Many functions have the same name in R and Python. In Python, they're often
methods instead of functions, so always check the methods on an object!


## Things That Are Different

This is a non-exhaustive list, so don't be surprised if things are missing.

Notation:

* `x`, `y` denote values (often sequences)
* `f` denotes a function
* `a`, `b`, `c` denote scalars
* `A`, `B` denote matrices
* `df`, `df2` denote data frames

### Core

R                    | Python              | Description
--------             | ----                | --
`?f`                 | `help(f)`           | Get help
`1+1i`               | `1+1j`              | Complex numbers
`2^3`                | `2**3`              | Exponentiation
`4 %% 2`             | `4 % 2`             | Remainder after division (modulus)
`!x`                 | `not x`             | Complement
`!x`                 | `~x`                | Complement (NumPy)
`typeof(42)`         | `type(42)`          | Get type
`class(42)`          | `type(42)`          | Get class (Python classes are types)
`f = function()`     | `def f():`          | Create function
`list("a", "b")`     | `["a", "b"]`        | Create list
`list(a = 3)`        | `{"a": 3}`          | Create dictionary
`seq(0, 9)`          | `range(10)`         | Create integer sequence
`seq_len(10)`        | `range(1, 11)`      | Create integer sequence
`seq.along(x)`       | `enumerate(x)`      | Enumerate sequence
`do.call(f, x)`      | `f(*x)`             | Call function with arguments in list
`lapply(f, x)`       | `map(f, x)`         | Functional map
`which(x)`           | `np.where(x)`       | Get indexes of non-false values
`names(x)`           | `x.keys()`          | Get names of dictionary keys
`"hi" %in% x`        | `"hi" in x`         | Check for value in list
`"hi" %in% names(x)` | `"hi" in x`         | Check for key in dictionary
`as.integer(x)`      | `int(x)`            | Cast scalar to integer
`as.double(x)`       | `float(x)`          | Cast scalar to floating point
`as.complex(x)`      | `complex(x)`        | Cast scalar to complex
`as.character(x)`    | `str(x)`            | Cast scalar to string
`as.list(x)`         | `list(x)`           | Cast to list
`message("Hi!")`     | `print("Hi!")`      | Print to console
`rev(x)`             | `reversed(x)`       | Reverse a sequence
`browser()`          | `breakpoint()`      | Run debugger (Python >= 3.7)
`table(x)`           | `x.value_counts()`  | Count elements (pandas)
`table(x, y)`        | `pd.crosstab(x, y)` | Crosstabulate elements

### Indexing and Slicing

* Starting Index
    + R: indexes start from 1.
    + Python: indexes start from 0.

* Negative Indexes
    + R: negative indexes are excluded, so `x[-1]` returns all except the first
      element.
    + Python: negative indexes count from the end, so `x[-1]` returns the last
      element (first from the end).

* Slices
    + R: `a:b` creates a sequence from `a` up to and including `b` with step
      size 1.
    + Python: `a:b` denotes the slice from `a` up to but excluding `b` with
      step size 1. Slices are not valid outside of the indexing operator `[ ]`.
        - Use `:b` to slice from beginning up to but excluding `b`.
        - Use `a:` to slice from `a` up to end.
        - Use `a:b:c` syntax to set step size `c`. Negative step sizes reverse
          the order of the result.

* Keeping Dimensions / Empty Slices
    * R: keep an entire dimension with a blank, as in `x[, 1]` to keep all rows
      and first column.
    * Python: keep an entire dimension with the empty slice `:`, as in 
      `x[:, 0]` to keep all rows and first column.


### Linear Algebra

R                           | Python                   | Description
--------                    | ----                     | --
`c(1, 2)`                   | `np.array([1, 2])`       | Create vector
`c(x, y)`                   | `np.concatenate([x, y])` | Combine vectors
`seq(0, 9)`                 | `np.arange(10)`          | Create integer sequence
`seq(0, 1, length.out = 5)` | `np.linspace(0, 1, 5)`   | Create decimal sequence
`length(x)`                 | `len(x)`                 | Vector length
`length(A)`                 | `A.size`                 | Matrix size
`dim(A)`                    | `A.shape`                | Dimensions
`ndim(A)`                   | `A.ndim`                 | Number of dimensions
`A %*% B`                   | `A @ B`                  | Matrix multiplication
`t(A)`                      | `A.T`                    | Transpose
`typeof(x)`                 | `x.dtype`                | Get vector type
`as.integer(x)`             | `x.astype("int64")`      | Cast vector to integer
`as.double(x)`              | `x.astype("float64")`    | Cast vector to floating point
`as.complex(x)`             | `x.astype("complex64")`  | Cast vector to complex


### Data Frames

R                     | Python                        | Description
--------              | ----                          | --
`data.frame()`        | `pd.DataFrame()`              | Create data frame
`read.csv()`          | `pd.read_csv()`               | Read CSV file
`df$my_col`           | `df.my_col`                   | Get column
`sapply(class, df)`   | `df.dtypes`                   | Get column types
`colnames(df)`        | `df.columns`                  | Get/set column names
`rownames(df)`        | `df.index`                    | Get/set row names
`rownames(df) = NULL` | `df.reset_index(drop = True)` | Reset row names
`str(df)`             | `df.info()`                   | Summarize structure
`summary(df)`         | `df.describe()`               | Summarize content
`rbind(x, y)`         | `pd.concat([x, y])`           | Bind rows
`cbind(x, y)`         | `pd.concat([x, y], axis = 1)` | Bind columns
`is.na(df)`           | `df.isna()`                   | Detect missing values
`split(df, groups)`   | `df.groupby(groups)`          | Group by
`df[1, 3]`            | `df.iloc[0, 2]`               | Index by location
`df[, "my_col"]`      | `df.loc[:, "my_col"]`         | Index by name
`df[condition, ]`     | `df.loc[condition, :]`        | Index by Boolean
`sapply(df, f)`       | `df.apply(f)`                 | Functional map over columns
`apply(df, 1, f)`     | `df.apply(f, axis = 1)`       | Functional map over rows

### Strings

R                      | Python                   | Description
--------               | ----                     | --
`nchar("Hi")`          | `len("Hi")`              | String length
`paste0("Hi", "hi")`   | `"Hi" + "hi"`            | Concatenate strings
`paste("Hi", "hi")`    | `" ".join(["Hi", "hi"])` | Concatenate strings
`tolower("Hi")`        | `"Hi".lower()`           | Convert to lowercase
`toupper("Hi")`        | `"Hi".upper()`           | Convert to uppercase
`trimws(x)`            | `x.strip()`              | Trim whitespace
`strsplit("1x2", "x")` | `"1x2".split("x")`       | Split string

Python string methods can be used on whole Pandas columns through the `.str`
attribute, as in `df["my_col"].str.lower()`.


#### Strings with stringr

Many of these are also available in base R.

R              | Python      | Description
--------       | ----        | --
`str_trim(x)`  | `x.strip()` | Trim whitespace
`str_split(x)` | x.split()`  | Split string
