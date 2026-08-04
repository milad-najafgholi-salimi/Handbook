![pic-89](89.png)

### Note:
><> is the standard SQL notation for “not equal”. != is an alias, which is converted to <> at a very early stage of parsing. Hence, it is not possible to implement != and <> operators that do different things.

As shown above, all comparison operators are binary operators that return values of type `boolean`. Thus, expressions like 1 < 2 < 3 are not valid (because there is no < operator to compare a Boolean value with 3). Use the `BETWEEN` predicates shown below to perform range tests.

![pic-90](90.png)

![pic-91](91.png)

![pic-92](92.png)

![pic-93](93.png)

The `BETWEEN` predicate simplifies range tests:

![pic-94](94.png)

To check whether a value is or is not null, use the predicates:

![pic-95](95.png)

![pic-96](96.png)

Do **not** write `expression = NULL` because `NULL` is not “equal to” `NULL`. (The null value represents an unknown value, and it is not known whether two unknown values are equal.)

