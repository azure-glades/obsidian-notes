

## Working with RStudio
- Source executes the .R file
- Source with echo executes the .R file along with commands
```R
a=11
b<-a*10
print(c(a,b)) #comment
```
Source, command window:
```R
> source("~/Coding/r/script1.R")
[1]  11 110
```
Source with echo, command window:
```R
> source("~/Coding/r/script1.R", echo=TRUE)
> a=11
> b<-a*10
> print(c(a,b)) #comment
[1]  11 110
```
Saving and loading environment variables:
```R
> save.image()
> load("~/Coding/r/script1.Rdata.RData")
```

## Variables
Valid names: var1, var_45, var.second
Non valid names: 1var, bar$, ghg#
constants: Pi
## Data types
1. Logical
2. Integer
3. Numeric
4. Complex
5. Character

suppose a variable `var`
`typeof(var)` - show datatype of `var`
`is.character(var)` - check if var is a character
`as.complex(var)` - convert var to complex. Not all conversions are possible.

## Basic Objects
1. Vector : a ordered collection of same data type
2. List : ordered collection of objects
3. Data frame: generic tabular object

### Vector
Ordered collection of basic datatypes with a given length.
Ex:
```R
X = c(1.3,2.4,3.5,4.5)
# c() is concatenate. makes a vector X
```

### List
Ordered collection of objects
Ex:
```R
ID=c(1,2,3,4)
emp.name=c("m","b","g")
emp.num=4 # these var names can be anything
emp.list=list(ID,emp.name,emp.num)
print(emp.list)
```
Output
```R
> source("~/Coding/r/script1.R")
[[1]]
[1] 1 2 3 4

[[2]]
[1] "m" "b" "g"

[[3]]
[1] 4
```
Elements of the list can be defined specifically
```R
emp.list=list("id"=ID,"names"=emp.name,"total staff"=emp.num)
```
They can be accessed as:
The `[[]]` operator is called *double slicing operator*
```R
print(emp.list$names) # access names
print(emp.list[[1]])  # access via index
```
>***Indexing in R starts from 1***
```R
print(emp.list[[2]][1]) # access 1st element from names
```
Can also be modified as 
```R
emp.list$id[4]=7
emp.list[[2]][1]= "jh"
```

Lists can be concatenated
```R
emp.ages=list("age"=c(23,24,54,53))
emp.list=c(emp.list,emp.ages)
```

### Data frame
Generic data object used to store tabular data. Each column in a data frame is a vector. A df is list of vectors
Ex:
```R
vec1 = c(1,2,3)
vec2 = c("R","C","C++")
vec3=c(4,7,18)
df=data.frame("rank"=vec1,"lang"=vec2,"complexity"=vec3,"power"=c(25,58,42))
print(df)

```
Output:
```R
> source("~/Coding/r/dataframescript.R")
  rank lang complexity power
1    1    R          4    25
2    2    C          7    58
3    3  C++         18    42
```

Data frames can be created by reading data from a file using
`df = read.table("/path")`
also specified with separator as `df = read.table(file="/path",sep)`

A specific element in a df can be referred with `df[row_num,col_num]` where it can be a range too
Ex:
```R
df[1,2]
df[1:4,]
df[,2:6]
df[,]
```

A subset of data can be extracted with `subset()`
```R
pd=subset(df,lang=="C")
print(pd)
```
Output:
```R
  rank lang complexity power
2    2    C          7    58
```
Here, pd is another dataframe. ![[Pasted image 20250114154411.png]]
Entries in df can also be changed like lists
```R
df[[2]][2] = "clang" # first index is column number, 2nd index is row number
```

Extra rows and columns can be added with `rbind(df,entries)` and `cbind(df, entries)`
```R
df=rbind(df,data.frame(rank=4,lang="MATLAB",complexity=5,power=48))
df=cbind(df,"age"=c(20,48,34,15))
```
Adding an extra element in column throws an error `error in data.frame(..., check.names = FALSE) : arguments imply differing number of rows: 4, 5`

Rows and columns can also be deleted by assigning negative/false indices
Ex:
```R
df1 = df[-3,-1]
df2 = df[,!df$lang=="MATLAB"] # MATLAB is in 4th row, so it deletes the 4th column
df3 = df[!df$lang=="MATLAB",] # deletes the row whcih has MATLAB
```

The **factor issue**, sometimes NA will show up when changing strings/characters. To avoid this, the definition has to be changed
```R
df = data.frame(vec1,vec2,vec3,, stringsAsFactors=F)
```

## Recasting Data frames
Manipulating a df in terms of its variables, i.e reshapes the data to better show specific aspects of data.
- Identifier variables - discreet variables
- Measurement variabler - numeric variables (cannot be categorical or data-time variables)
Done with `melt()` and `cast()` which is from `reshape2` library
(Load a library with: `library(reshape2)`)
Syntax:
- `melt(dataframe, id.vars, measure.vars, variable.name = "var", value.name= "value")`
 - `dcast(dataframe, formula, value.var = {col with values})`
 ex:
 ```R
meltdf = melt(df,id.vars = c("lang","maker"), measure.vars = c("complexity","power"))
print(meltdf)
castdf = dcast(meltdf, variable+maker ~ lang, value.var="value")
print(castdf)
```

melt and cast can be combined with `recast()`. Syntax:
- `recast(dataframe, formula, id.vars, measure.vars)`
ex:
```R
redf = recast(df, variable+maker ~ lang, id.var=c("lang","maker"), measure.var=c("complexity","power"))
print(redf) # equivalent to melt and dcast
```

New field can be added to data frame using `mutate()` from `dplyr` library
Syntax: `mutate(df, name = func(field)`
```R
library(dplyr)

nameVec=c("Alice","Alice","Bob","Bob")
monthVec=c("Jan","Feb","Jan","Feb")
BSVec=c(141.2,139.3,135.2,160.1)
BPVec=c(108,114,82,96)

df = data.frame("name" = nameVec, "month"=monthVec,"bs"=BSVec, "bp"=BPVec)
# print(df)

ndf <- mutate(df,"log of bp" = log(bp))
print(ndf)
```

## Joining data frames
- To join data in 2 dataframes, a suitable common field has be present between them
Done using `dplyr` library
Syntax: `join(df1, df2, by= id.vars)`
```R
library(dplyr)

nameVec=c("Alice","Alice","Bob","Bob","Jon","Jon")
monthVec=c("Jan","Feb","Jan","Feb","Jan","Feb")
BSVec=c(141.2,139.3,135.2,160.1,144,135.3)
BPVec=c(108,114,82,96,100,102)

df1 = data.frame("name" = nameVec, "month"=monthVec,"bs"=BSVec, "bp"=BPVec)
# print(df1)
df1 <- mutate(df1,"log of bp" = log(bp))
# print(ndf)

df2 = data.frame("name"=c("Alice","Bob","Sam"),"age"=c(34,35,22))
# print(df2)
ndf = left_join(df1,df2,by="name")
print(ndf)

mdf = right_join(df1,df2,by="name")
print(mdf)

idf = inner_join(df1,df2,by="name")
print(idf)

```

`left_join()` combines data in df2 with df1 (all data in df1 is retained)
`right_join()` combines data in df1 with df2 (all data in df1 is retained)
`inner_join()`  combines data that is present in both dfs