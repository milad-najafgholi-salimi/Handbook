- There are three number types in R:
    * numeric
    * integer
    * complex
* Variables of number types are created when you assign a value to them:
```
x <- 10.5 [or] x <- 12          # numeric
y <- 10L  [wrong: y <- 10.5L]   # integer
z <- 1i   [Also: z <- 3 + 5i]   # complex
```
---
#### Type Conversion
- You can convert from one type to another with the following functions:
    * as.numeric()
    * as.integer()
    * as.complex()

Example:
```
x <- 1L     # integer
y <- 2      # numeric

# convert from integer to numeric:
a <- as.numeric(x)

# convert from numeric to integer:
b <- as.integer(y)

# print values of x and y
x
y

# print the class name of a and b
class(a)
class(b)
