- To assign a value to a variable, use the `<-` sign. To output (or print) the variable value, just type the variable name. - Example:
```
name <- "Milad"
age <- 22

name    # output: "Milad"
age     # output: 22
```
- In other programming language, it is common to use `=` as an assignment operator. 
In R, we can use both `=` and `<-` as assignment operators.
However, `<-` is preferred in most cases because the `=` operator can be forbidden in some contexts in R.

---
#### Concatenate Elements
- You can also concatenate, or join, two or more elements, by using the `paste()` function. - Example:
```
text <- "good"
paste("R is", text)
```
Example:
```
txt_1 <- "R is"
txt_2 <- "good"
paste(txt_1, txt_2)
```
- For numbers, the `+` character works as a mathematical operator. - Example:
```
num1 <- 3
num2 <- 5

num1 + num2
```
If you try to combine a string (text) and a number, R will give you an error.
Also combine two strings, R will give you an error. - Example:
```
txt <- "good"
txt_1 <- "R is"
paste(txt_1 + txt)

# """ This will give you and error """
```
---
#### Multiple Variables
- R allows you to assign the same value to multiple variables in one line. - Example:
```
var1 <- var2 <- var3 <- "Milad"
var1
var2
var3

# output:
	"Milad"
	"Milad"
	"Milad"
```
