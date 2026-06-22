- A string is surrounded by either single quotation marks, or double quotation marks:
"hello" is the same as 'hello'.
---
#### Multiline Strings
- You can assign a multiline string to a variable like this - Example:
```
str <- "Hi. I'm Milad. I'm a junior data scientist at the present. I always learn and practice to learn more and more. I hope one day AI become super smart and be our friends."

str     # print the value of str
```
However, note that R will add a `"\n"` at the end of each line break. This is called an escape character, 
and the `n` character indicates a new line.
- If you want the line breaks to be inserted at the same position as in the code, use the `cat()` function. - Example:
```
str <- "Hi. I'm Milad. I'm a junior data scientist at the present. I always learn and practice to learn more and more. I hope one day AI become super smart and be our friends."

cat(str)
```
------------
#### String Length
- There are many useful string functions in R.
- For example, to find the number of characters in a string, use the `nchar()` function - Example:
```
str <- "Hello World!"
nchar(str)
```
---
#### Check a String
- Use the `grepl()` function to check if a character or a sequence of characters are present in a string - Example:
```
str <- "Hello World!"

grepl("H", str)         # output: TRUE
grepl("Hello", str)     # output: TRUE
grepl("x", str)         # output: FALSE
```
---
#### Combine Two Strings
- Use the `paste()` function to merge/concatenate two strings - Example:
```
str1 <- "Hello"
str2 <- "World"

paste(str1, str2)
```
---
#### Escape Characters
- To insert characters that are illegal in a string, you must use an escape character.
- An escape character is a backslash `\` followed by the character you want to insert.
