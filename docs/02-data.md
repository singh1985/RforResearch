---
output:
  html_document: default
  pdf_document: default
  header-includes:
    - \usepackage{caption}
---


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
[1] TRUE
```

### Integer

- Integers are natural numbers. 


```r
x=9
typeof(x)
```

```
[1] "double"
```



```r
#The following specifically assigns an integer to x

x=as.integer(9)
typeof(x)
```

```
[1] "integer"
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
[1] TRUE
```

```r
typeof(a)
```

```
[1] "logical"
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
[1] A  AB B  O 
Levels: A AB B O
```

```r
#to get individual elements (levels) in factor object
levels(b.type)
```

```
[1] "A"  "AB" "B"  "O" 
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
[1] "2012-01-31"
```

```r
data.class(date1)
```

```
[1] "Date"
```

```r
#The date and time are internally interpreted as Double so the function typeof will return the type Double
typeof(date1)
```

```
[1] "double"
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
[1] 1 2 3 4 5
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
     [,1] [,2]
[1,]    1    2
[2,]    3    4
[3,]    5    6
```


- A vector can be converted to matrix using $\mathtt{dim}$ function, e.g:


```r
m2=c(1,2,3,4,5,6)
dim(m2)=c(3,2)#the matrix will be filled by columns
m2
```

```
     [,1] [,2]
[1,]    1    4
[2,]    2    5
[3,]    3    6
```

```r
#use dim to get the dimension (#rows and #columns) of a matrix
dim(m1) 
```

```
[1] 3 2
```

** Matrix Manipulations **

- For calculations on matrices; all the mathematical functions available for vectors are applicable on a matrix. All operations are applied on each element in a matrix, e.g.


```r
m3=m1*2 # all elements will be multiplied by 2 individually
m3
```

```
     [,1] [,2]
[1,]    2    4
[2,]    6    8
[3,]   10   12
```

- A matrix can be multiplied with a vector as long as the length of the vector is a multiple of length of the matrix. Try different combinations of matrix and vector arithmetic to see the results and errors. 

- Mathematical matrix operations are also available for matrices in R. For instance $\mathtt{\%*\%}$ is used for matrix multiplication, the matrices must agree dimensionally for matrix multiplication. Note the use of $\mathtt{:}$ operator to create a sequence.


```r
dim(m1)# 3 rows and 2 columns
```

```
[1] 3 2
```

```r
#create another matrix with 2 rows and 3 columns
m3=matrix(c(1:6),ncol=3)
m1%*%m3
```

```
     [,1] [,2] [,3]
[1,]    5   11   17
[2,]   11   25   39
[3,]   17   39   61
```

R facilitates various matrix specific operations. Table 1 gives most of the available functions and operators. Use $\mathtt{help()}$ or $\mathtt{?}$ followed by function name to get more details about the operators and functions. 

<div class='float-table'><div class="plain_layout" id='magicparlabel-976'><span class='float-caption-Standard float-caption float-caption-standard'>Table :  Functions and operators for matrices</span></div>
<div class="plain_layout" style='text-align: left;' id='magicparlabel-981'><table><tbody><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1040'><b>Operator or Function</b></div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1043'><b>Description</b></div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1046'>X * Y </div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1049'>Element-wise multiplication</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1052'>X %*% Y</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1055'>Matrix multiplication</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1058'>Y %o% X </div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1061'>Outer product. XB' </div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1064'>crossprod(X,Y)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1067'>X'Y </div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1070'>crossprod(X)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1073'> X'X</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1076'>t(X) </div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1079'>Transpose</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1082'>diag(x)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1085'>Creates diagonal matrix with elements of x in the principal diagonal</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1088'>diag(X)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1091'>Returns a vector containing the elements of the principal diagonal</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1094'>diag(k)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1097'>If k is a scalar, this creates a k x k identity matrix. Go figure.</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1100'>solve(X, b)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1103'>Returns vector x in the equation b = Xx (i.e., X-1b)</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1106'>solve(X)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1109'>Inverse of X where X is a square matrix.</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1112'>y=eigen(X)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1115'>y$val are the eigenvalues of X</div>
</td>
</tr><tr><td align='left' valign='top'>

</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1121'>y$vec are the eigenvectors of X</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1124'>y=svd(X)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1127'>Singular value decomposition of X.</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1130'>R = chol(X)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1133'>Choleski factorization of X. Returns the upper triangular factor, such that R'R = X.</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1136'>y = qr(X) </div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1139'>QR decomposition of X.</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1142'>cbind(X,Y,...)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1145'>Combine matrices(vectors) horizontally. Returns a matrix.</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1148'>rbind(X,Y,...)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1151'>Combine matrices(vectors) vertically. Returns a matrix.</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1154'>rowMeans(X)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1157'>Returns vector of row means.</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1160'>rowSums(X)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1163'>Returns vector of row sums.</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1166'>colMeans(X)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1169'>Returns vector of column means.</div>
</td>
</tr><tr><td align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1172'>colSums(X)</div>
</td>
<td style ="width: 9cm;" align='left' valign='top'>
<div class="plain_layout" id='magicparlabel-1175'>Returns vector of column means.</div>
</td>
</tr></tbody>
</table>
</div>
</div>


### Arrays

- Arrays are the generalisation of vectors and matrices. A vector in R is a one dimensional array and a matrix a two dimensional array. An array is a multiply subscripted collection of data entries of the same data type. Arrays can be constructed using the function $\mathtt{array}$, for example[^5] 

[^5]: Function $\mathtt{dim}$ can also be used to define an array by assigning dimensions to a vector.


```r
z=c(1:24)#vector of length 24
#constructing a 3 by 4 by 2 array
a1=array(z,dim=c(3,4,2)) 
a1
```

```
, , 1

     [,1] [,2] [,3] [,4]
[1,]    1    4    7   10
[2,]    2    5    8   11
[3,]    3    6    9   12

, , 2

     [,1] [,2] [,3] [,4]
[1,]   13   16   19   22
[2,]   14   17   20   23
[3,]   15   18   21   24
```

- Individual elements of an array are accessed by referring them by their index. This is done by giving the name of the array followed by the subscript (index) in this square bracket separated by commas. We try to access the element [1,3,1] of array a1 in the following example 


```r
#element in the row 1 and column 3 in the first subset
a1[1,3,1]
```

```
[1] 7
```


### Data Frames
- Data frame forms the most convenient data structures in R to represent tabular data. 

- In quantitative research data is often in the form of data tables. These data tables have multiple rows and can have multiple columns with each column representing a different variable (quantity). 

- A data frame in R is the most natural way to represent these data sets as it can have different data type in the data frame object. Most statistical routines in R require a data frame as input. 

The following example uses an important function $\mathtt{str}$ on R's inbuilt data frame “swiss”. $\mathtt{str}$ function is used to see the internal structure of an object in R. 


```r
options(str=list(vec.len=2))
#swiss dataframe has standardized fertility measure and socio-economic indicators 
#for each of 47 French-speaking provinces of Switzerland at about 1888.
data(swiss)
str(swiss)
```

```
'data.frame':	47 obs. of  6 variables:
 $ Fertility       : num  80.2 83.1 92.5 85.8 76.9 ...
 $ Agriculture     : num  17 45.1 39.7 36.5 43.5 ...
 $ Examination     : int  15 6 5 12 17 ...
 $ Education       : int  12 9 5 7 15 ...
 $ Catholic        : num  9.96 84.84 ...
 $ Infant.Mortality: num  22.2 22.2 20.2 20.3 20.6 ...
```

- Data frames have two attributes namely; $\mathtt{names}$ and $\mathtt{row.names}$, these two contains the column names and row names respectively. The data in the named column can be accessed by the $\mathtt{\$}$ operator. 


```r
#using names and row.names
names(swiss)#name of the columns (can also use colnames)
```

```
[1] "Fertility"        "Agriculture"      "Examination"      "Education"       
[5] "Catholic"         "Infant.Mortality"
```

```r
colnames(swiss)
```

```
[1] "Fertility"        "Agriculture"      "Examination"      "Education"       
[5] "Catholic"         "Infant.Mortality"
```

```r
row.names(swiss)#name of the rows
```

```
 [1] "Courtelary"   "Delemont"     "Franches-Mnt" "Moutier"      "Neuveville"  
 [6] "Porrentruy"   "Broye"        "Glane"        "Gruyere"      "Sarine"      
[11] "Veveyse"      "Aigle"        "Aubonne"      "Avenches"     "Cossonay"    
[16] "Echallens"    "Grandson"     "Lausanne"     "La Vallee"    "Lavaux"      
[21] "Morges"       "Moudon"       "Nyone"        "Orbe"         "Oron"        
[26] "Payerne"      "Paysd'enhaut" "Rolle"        "Vevey"        "Yverdon"     
[31] "Conthey"      "Entremont"    "Herens"       "Martigwy"     "Monthey"     
[36] "St Maurice"   "Sierre"       "Sion"         "Boudry"       "La Chauxdfnd"
[41] "Le Locle"     "Neuchatel"    "Val de Ruz"   "ValdeTravers" "V. De Geneve"
[46] "Rive Droite"  "Rive Gauche" 
```

```r
swiss$Fertility #returns the vector of data in the column Fertility
```

```
 [1] 80.2 83.1 92.5 85.8 76.9 76.1 83.8 92.4 82.4 82.9 87.1 64.1 66.9 68.9 61.7
[16] 68.3 71.7 55.7 54.3 65.1 65.5 65.0 56.6 57.4 72.5 74.2 72.0 60.5 58.3 65.4
[31] 75.5 69.3 77.3 70.5 79.4 65.0 92.2 79.3 70.4 65.7 72.7 64.4 77.6 67.6 35.0
[46] 44.7 42.8
```

- Data frames are constructed using the function $\mathtt{data.frame}$. For example following creates a data frame of a character and numeric vector. 


```r
num1=seq(1:5)
ch1=c("A","B","C","D","E")
df1=data.frame(ch1,num1)
df1
```

```
  ch1 num1
1   A    1
2   B    2
3   C    3
4   D    4
5   E    5
```

### Lists
- A list is like generic vector containing other objects. Lists can have numerous elements any type and structure they can also be of different lengths

- A list can contain another list and therefore it can be used to construct arbitrary data structures.  

- A list can be constructed using the $\mathtt{list}$ function, for example


```r
e1 = c(2, 3, 5) #element-1
e2 = c("aa", "bb", "cc", "dd", "ee")  #element-2
e3 = c(TRUE, FALSE, TRUE, FALSE, FALSE)#element-3
e4=df1 #element-4 (previously constructed data frame)
lst1 = list(e1,e2,e3, e4)   # lst contains copies of e1,e2,e3,e4
str(lst1)#show the structure of lst1
```

```
List of 4
 $ : num [1:3] 2 3 5
 $ : chr [1:5] "aa" "bb" ...
 $ : logi [1:5] TRUE FALSE TRUE ...
 $ :'data.frame':	5 obs. of  2 variables:
  ..$ ch1 : chr [1:5] "A" "B" ...
  ..$ num1: int [1:5] 1 2 3 4 5
```


- Components are always numbered and may always be referred to as such.
<div class="figure">
<img src="CO2_qPVWsAAErbv.png large.png" alt="Lists" width="687" />
<p class="caption">(\#fig:unnamed-chunk-19)Lists</p>
</div>

- Thus if lst1 is the name of a list with four components, these may be individually referred to as lst1[[1]], lst1[[2]], lst1[[3]] and lst1[[4]]. Note: When a single square bracket is used the component of a list is returned as a list while the double square bracket returns the component itself


```r
#first element of lst1
lst1[[1]]
```

```
[1] 2 3 5
```

```r
lst1[1]
```

```
[[1]]
[1] 2 3 5
```

- The elements in a list can also be named using the \mathtt{list} function and these elements can be referred individually via there names. 



```r
names(lst1)=c("e1","e2","e3","e4")
names(lst1)#name of the elements
```

```
[1] "e1" "e2" "e3" "e4"
```

```r
lst1$e1 #using $operator to refer the element
```

```
[1] 2 3 5
```

> This section provided an overview of various data types and data structures in R. The next section will discuss how to deal with external data souces with flat data.
