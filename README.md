1. R Expressions &amp; Data Structures

Program:

Expression &lt;- function(x,y)
{
obj &lt;- list(X=x, Y=y, Result=NULL)
class(obj) &lt;- &quot;Expression&quot;
return(obj)
}
evaluate.Expression &lt;- function(obj)
{
obj$Result &lt;- obj$X^2 + obj$Y^2
return(obj)
}
print.Expression &lt;- function(obj)
{
cat(&quot;X:&quot;, obj$X, &quot; Y:&quot;, obj$Y, &quot;\n&quot;)
cat(&quot;Result (x^2 + y^2):&quot;, obj$Result, &quot;\n&quot;)
}
exp1 &lt;- Expression(10,5)
exp1 &lt;- evaluate.Expression(exp1)
print(exp1)

Output:

2. Manipulation of Vectors and Matrices

Program:

setClass(&quot;MathData&quot;,
slots = list(Vec = &quot;numeric&quot;, Mat = &quot;matrix&quot;))
setGeneric(&quot;vectorOps&quot;, function(object) standardGeneric(&quot;vectorOps&quot;))
setMethod(&quot;vectorOps&quot;, &quot;MathData&quot;, function(object){
cat(&quot;Vector Elements:&quot;, object@Vec, &quot;\n&quot;)
cat(&quot;First Element:&quot;, object@Vec[1], &quot;\n&quot;)
cat(&quot;Subset (2nd to 4th):&quot;, object@Vec[2:4], &quot;\n&quot;)
cat(&quot;Sum of Vector:&quot;, sum(object@Vec), &quot;\n&quot;)
cat(&quot;Mean of Vector:&quot;, mean(object@Vec), &quot;\n&quot;)
cat(&quot;Sorted Vector:&quot;, sort(object@Vec), &quot;\n\n&quot;)
})
setGeneric(&quot;matrixOps&quot;, function(object) standardGeneric(&quot;matrixOps&quot;))
setMethod(&quot;matrixOps&quot;, &quot;MathData&quot;, function(object){
cat(&quot;Matrix:\n&quot;); print(object@Mat)
cat(&quot;\nTranspose:\n&quot;); print(t(object@Mat))
cat(&quot;\nFirst Row:&quot;, object@Mat[1,], &quot;\n&quot;)
cat(&quot;Second Column:&quot;, object@Mat[,2], &quot;\n&quot;)
cat(&quot;\nMatrix Multiplication (Mat %*% t(Mat)):\n&quot;)
print(object@Mat %*% t(object@Mat))
})
vec_input &lt;- as.numeric(unlist(strsplit(readline(prompt=&quot;Enter vector elements separated
by space: &quot;), &quot; &quot;)))
mat_input &lt;- matrix(as.numeric(unlist(strsplit(readline(prompt=&quot;Enter 9 numbers for 3x3
matrix: &quot;), &quot; &quot;))),
nrow=3, byrow=TRUE)
md &lt;- new(&quot;MathData&quot;, Vec = vec_input, Mat = mat_input)
vectorOps(md)
matrixOps(md)

Output:

3. Operators on Factors in R

Program:

Category &lt;- function(items){
obj &lt;- list(Items = factor(items)) # Store as factor
class(obj) &lt;- &quot;Category&quot; # Assign S3 class
return(obj)
}
analyze.Category &lt;- function(obj){
cat(&quot;Factor Items:\n&quot;); print(obj$Items)

cat(&quot;\nLevels of Factor:\n&quot;); print(levels(obj$Items))

cat(&quot;\nFrequency Count:\n&quot;); print(summary(obj$Items))

cat(&quot;\nSorted Factor:\n&quot;); print(sort(obj$Items))

cat(&quot;\nReordered Factor (reverse levels):\n&quot;)
new_fac &lt;- factor(obj$Items, levels = rev(levels(obj$Items)))
print(new_fac)
}
user_items &lt;- unlist(strsplit(readline(prompt=&quot;Enter categories separated by space: &quot;), &quot; &quot;))
catObj &lt;- Category(user_items)
analyze.Category(catObj)

Input:

Enter categories separated by space: apple banana orange apple banana

Output:

4. Data Frames in R

Program:
StudentData &lt;- function(ids, names, marks){
obj &lt;- list(
DF = data.frame(ID = ids, Name = names, Marks = marks)
)
class(obj) &lt;- &quot;StudentData&quot; # Assign S3 class
return(obj)
}
analyze.StudentData &lt;- function(obj){
cat(&quot;Original Data Frame:\n&quot;)
print(obj$DF)

cat(&quot;\nAccessing 1st Row:\n&quot;)
print(obj$DF[1, ])
cat(&quot;\nAccessing &#39;Name&#39; Column:\n&quot;)
print(obj$DF$Name)
cat(&quot;\nAdding Grade Column:\n&quot;)
obj$DF$Grade &lt;- ifelse(obj$DF$Marks &gt;= 90, &quot;A&quot;,
ifelse(obj$DF$Marks &gt;= 75, &quot;B&quot;, &quot;C&quot;))
print(obj$DF)
cat(&quot;\nFiltering Students with Marks &gt;= 80:\n&quot;)
print(subset(obj$DF, Marks &gt;= 80))
cat(&quot;\nStatistical Summary of Marks:\n&quot;)
print(summary(obj$DF$Marks))
}
ids &lt;- as.integer(unlist(strsplit(readline(&quot;Enter student IDs separated by space: &quot;), &quot; &quot;)))
names &lt;- unlist(strsplit(readline(&quot;Enter student names separated by space: &quot;), &quot; &quot;))
marks &lt;- as.numeric(unlist(strsplit(readline(&quot;Enter student marks separated by space: &quot;), &quot;
&quot;)))
studObj &lt;- StudentData(ids, names, marks)

analyze.StudentData(studObj)
Output:

5. Lists and operators

Program:
Document&lt;-function(text){
obj&lt;-list(Text=text,Words=unlist(strsplit(tolower(text),&quot;\\s+&quot;)))
class(obj)&lt;-&quot;Document&quot;
return(obj)
}
wordcount.Document&lt;-function(obj){
tbl&lt;-table(obj$Words)
return(tbl)
}
print.Document&lt;-function(obj){
cat(&quot;Document:&quot;,obj$Text,&quot;\n&quot;)
print(wordcount.Document(obj))
}
doc1&lt;-Document(&quot;Data science is powerful and data is everywhere&quot;)
print(doc1)

Output:

6. Working with Looping Statements in R

Program:
LoopDemo &lt;- function(nums, factNum){
obj &lt;- list(
Numbers = nums,
FactorialNumber = factNum
)
class(obj) &lt;- &quot;LoopDemo&quot;
return(obj)
}
process &lt;- function(obj) {
UseMethod(&quot;process&quot;)
}
process.LoopDemo &lt;- function(obj){
total &lt;- 0
for(i in obj$Numbers){
total &lt;- total + i
}
cat(&quot;Sum of Numbers using for loop:&quot;, total, &quot;\n&quot;)
n &lt;- obj$FactorialNumber
fact &lt;- 1
while(n &gt; 0){
fact &lt;- fact * n
n &lt;- n - 1
}
cat(&quot;Factorial using while loop:&quot;, fact, &quot;\n&quot;)
cat(&quot;Numbers generated using repeat loop:\n&quot;)
x &lt;- 1
repeat{
cat(x, &quot; &quot;)
x &lt;- x + 2
if(x &gt; 20) break
}
cat(&quot;\n&quot;)
}
nums &lt;- c(1, 2, 3, 4, 5)
factNum &lt;- 5
loopObj &lt;- LoopDemo(nums, factNum)
process(loopObj)

Output:

7. Graphs in R

data(mtcars)
hist(mtcars$mpg,
main = &quot;Histogram of Miles per Gallon&quot;,
xlab = &quot;Miles per Gallon&quot;,
col = &quot;lightblue&quot;, border = &quot;black&quot;)
boxplot(mtcars$hp,
main = &quot;Boxplot of Horsepower&quot;,
ylab = &quot;Horsepower&quot;,
col = &quot;lightgreen&quot;)
plot(mtcars$hp, mtcars$mpg,
main = &quot;Scatterplot of MPG vs Horsepower&quot;,
xlab = &quot;Horsepower&quot;,
ylab = &quot;Miles per Gallon&quot;,
col = &quot;blue&quot;, pch = 19)
plot(mtcars$mpg,
type = &quot;o&quot;,
main = &quot;Line Chart of MPG across Cars&quot;,
xlab = &quot;Car Index&quot;,
ylab = &quot;Miles per Gallon&quot;,
col = &quot;red&quot;)

Output:

8. 3D plots in R

library(scatterplot3d)
x &lt;- 1:10
y &lt;- x^2
z &lt;- x^3
scatterplot3d(x, y, z,
main = &quot;3D Scatter Plot&quot;,
xlab = &quot;X axis&quot;,
ylab = &quot;Y axis&quot;,
zlab = &quot;Z axis&quot;,
color = &quot;blue&quot;,
pch = 19)
scatterplot3d(x, y, z, angle = 55)
s3d &lt;- scatterplot3d(x, y, z)
fit &lt;- lm(z ~ x + y) # linear model
s3d$plane3d(fit)
z &lt;- outer(x, y, function(x, y) cos(sqrt(x^2 + y^2)))
persp(x, y, z,
col = &quot;lightblue&quot;,
theta = 30, phi = 20, # rotation angles
expand = 0.5,
xlab = &quot;X&quot;, ylab = &quot;Y&quot;, zlab = &quot;Z&quot;,
main = &quot;3D Surface Plot (persp)&quot;)
