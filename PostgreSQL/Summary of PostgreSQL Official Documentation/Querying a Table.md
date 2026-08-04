To retrieve data from a table, the table is queried. An SQL `SELECT` statement is used to do this. The statement is divided into a select list (the part that lists the columns to be returned), a table list (the part that lists the tables from which to retrieve the data), and an optional qualification (the part that specifies any restrictions). For example, to retrieve all the rows of table `weather`, type:

![pic-6](PostgreSQL/Summary%20of%20PostgreSQL%20Official%20Documentation/imgs/6.png)

Here `*` is a shorthand for “all columns”. So the same result would be had with:

![pic-7](7.png)

You can write expressions, not just simple column references, in the select list. For example, you can do:

![pic-8](8.png)

This should give:

![pic-9](9.png)

Notice how the `AS` clause is used to relabel the output column. (The `AS` clause is optional.)

A query can be “qualified” by adding a `WHERE` clause that specifies which rows are wanted. The `WHERE` clause contains a Boolean (truth value) expression, and only rows for which the Boolean expression is true are returned. The usual Boolean operators (`AND`, `OR`, and `NOT`) are allowed in the qualification. For example, the following retrieves the weather of San Francisco on rainy days:

![pic-10](10.png)

Result:

![pic-11](11.png)

You can request that the results of a query be returned in sorted order:

![pic-12](12.png)

Result:

![pic-13](13.png)

In this example, the sort order isn't fully specified, and so you might get the San Francisco rows in either order. But you'd always get the results shown above if you do:

![pic-14](14.png)

You can request that duplicate rows be removed from the result of a query:

![pic-15](15.png)

Result:

![pic-16](16.png)

Here again, the result row ordering might vary. You can ensure consistent results by using `DISTINCT` and `ORDER` BY together:

![pic-17](17.png)

