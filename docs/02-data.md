# R Data Types and Data Structures

*When human judgement and big data intersect there are some funny things that happen.* 
-Nate Silver 

## Data Types

- As per R's official language definitions; in every computer language variables provide a means of accessing the data stored in memory. 

- R does not provide direct access to the computer's memory but rather provides a number of specialized data structures we will refer to as objects. These objects are referred to through symbols or variables. 

### Double

- Doubles are numbers like 5.0, 5.5, 10.999 etc. They may or may not include decimal places. Doubles are mostly used to represent a continuous variable like serial number, weight, age etc. 


```r
x=8.5
is.double(x) #to check if the data type is double
```

```
## [1] TRUE
```

### Integer

- Integers are natural numbers. 


```r
x=9
typeof(x)
```

```
## [1] "double"
```



```r
#The following specifically assigns an integer to x

x=as.integer(9)
typeof(x)
```

```
## [1] "integer"
```

### Logical

- A variable of data type logical has the value TRUE or FALSE. To perform calculation on logical objects in R the FALSE is replaced by a zero and TRUE is replaced by 1.


```r
x=11
y=10
a=x>y
a
```

```
## [1] TRUE
```

```r
typeof(a)
```

```
## [1] "logical"
```



### Character

- Characters represent the string values in R. An object of type character can have alphanumeric strings. Character objects are specified by assigning a string or collection of characters between double quotes (“ string”) . Everything in a double quote is considered a string in R.

### Factor
-Factor is an important data type to represent categorical data. This also comes handy when dealing with Panel or Longitudinal data. Example of factors are Blood type (A , B, AB, O), Sex (Male or Female). Factor objects can be created from character object or from numeric object. 
-The operator c is used to create a vector of values which can be of any data type.

```r
b.type=c("A","AB","B","O") #character object
#use factor function to convert to factor object
b.type=factor(b.type)
b.type
```

```
## [1] A  AB B  O 
## Levels: A AB B O
```

```r
#to get individual elements (levels) in factor object
levels(b.type)
```

```
## [1] "A"  "AB" "B"  "O"
```

### Date & Time
-R is capable of dealing calendar dates and times. It is an important object when dealing with time series models. The function `as.Date` can be used to create an object of class Date.
- see `help(as.Date)` for more details about the format of dates.


```r
date1="31-01-2012"
date1=as.Date(date1,"%d-%m-%Y")
date1
```

```
## [1] "2012-01-31"
```

```r
data.class(date1)
```

```
## [1] "Date"
```

```r
#The date and time are internally interpreted as Double so the function typeof will return the type Double
typeof(date1)
```

```
## [1] "double"
```

## Data Structures in R
Every data analysis requires the data to be structured in a well defined way. These coherent ways to put together data forms some basic data structures in R. Every data set intended for analysis has to be imported in R environment as a data structure. R has the following basic data structures:

• Vector

• Matrix

• Array

• Data Frame

• Lists


### Vector
- Vectors are group of values having same data types. 

- There can be numeric vectors, character vector and so on. Vectors are mostly used to represent a single variable in a data set. 

- A vector is constructed using the function `c`. The same function `c` can be used to combine different vectors of same data type.


```r
vec1=c(1,2,3,4,5)
vec1
```

```
## [1] 1 2 3 4 5
```
> The `str` function can be used to view the data structure of an object

### Matrices

- A matrix is a collection of data elements arranged in a two-dimensional rectangular layout. Like vectors all the elements in a matrix are of same data type. 

$\left[\begin{array}{cc}
1 & 2\\
3 & 4\\
5 & 6
\end{array}\right]$

-  The function $\mathtt{matrix}$ is used to create matrices in R. Note that all the elements in a matrix object are of same basic type. Lets create the matrix in the example above.



```r
m1=matrix(c(1,2,3,4,5,6),nrow=3,ncol=2,byrow=TRUE)
#nrow-specify number of rows,
#ncol-specify number of columns,
#byrow-fill the matrix in rows with the data supplied
m1 #print the matrix
```

```
##      [,1] [,2]
## [1,]    1    2
## [2,]    3    4
## [3,]    5    6
```


 
