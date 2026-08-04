The process of retrieving or the command to retrieve data from a database is called a query. In SQL the `SELECT` command is used to specify queries. The general syntax of the `SELECT` command is

![pic-63](63.png)

A simple kind of query has the form:

![pic-64](64.png)

![pic-65](65.png)

(assuming that b and c are of a numerical data type).

FROM table1 is a simple kind of table expression: it reads just one table. In general, table expressions can be complex constructs of base tables, joins, and subqueries. But you can also omit the table expression entirely and use the SELECT command as a calculator:

![pic-66](66.png)

This is more useful if the expressions in the select list return varying results. For example, you could call a function this way:

![pic-67](67.png)

