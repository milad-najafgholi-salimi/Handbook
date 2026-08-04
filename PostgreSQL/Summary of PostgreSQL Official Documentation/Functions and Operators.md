PostgreSQL provides a large number of functions and operators for the built-in data types. This chapter describes most of them, although additional special-purpose functions appear in relevant sections of the manual. Users can also define their own functions and operators, as described in Part V. The psql commands `\df` and `\do` can be used to list all available functions and operators, respectively.

The notation used throughout this chapter to describe the argument and result data types of a function or operator is like this:

![pic-85](85.png)

which says that the function repeat takes one text and one integer argument and returns a result of type text. The right arrow is also used to indicate the result of an example, thus:

![pic-86](86.png)

