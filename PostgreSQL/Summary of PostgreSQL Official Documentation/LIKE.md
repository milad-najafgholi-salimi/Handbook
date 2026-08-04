![pic-127](127.png)

The `LIKE` expression returns true if the `string` matches the supplied `pattern`. (As expected, the `NOT LIKE` expression returns false if `LIKE` returns true, and vice versa. An equivalent expression is `NOT` (`string LIKE pattern`).)

If `pattern` does not contain percent signs or underscores, then the pattern only represents the string itself; in that case `LIKE` acts like the equals operator. An underscore (`_`) in `pattern` stands for (matches) any single character; a percent sign `%` matches any sequence of zero or more characters. Some examples:

![pic-128](128.png)

`LIKE` pattern matching supports nondeterministic collations, such as case-in-sensitive collations or collations that, say, ignore punctuation. So with a case-insensitive collation, one could have:

![pic-129](129.png)

With collations that ignore certain characters or in general that consider strings of different lengths equal, the semantics can become a bit more complicated. Consider these examples:

![pic-130](130.png)

`LIKE` pattern matching always covers the entire string. Therefore, if it's desired to match a sequence anywhere within a string, the pattern must start and end with a percent sign.

