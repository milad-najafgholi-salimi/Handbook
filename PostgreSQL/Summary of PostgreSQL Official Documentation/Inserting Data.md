When a table is created, it contains no data. The first thing to do before a database can be of much use is to insert data. Data is inserted one row at a time. You can also insert more than one row in a single command, but it is not possible to insert something that is not a complete row. Even if you know only some column values, a complete row must be created.


To create a new row, use the INSERT command. The command requires the table name and column values.

![pic-45](45.png)

The above syntax has the drawback that you need to know the order of the columns in the table. To avoid this you can also list the columns explicitly. For example, both of the following commands have the same effect as the one above:

Many users consider it good practice to always list the column names.

If you don't have values for all the columns, you can omit some of them. In that case, the columns will be filled with their default values. For example:

![pic-47](47.png)

The second form is a PostgreSQL extension. It fills the columns from the left with as many values as are given, and the rest will be defaulted.

For clarity, you can also request default values explicitly, for individual columns or for the entire row:
![pic-48](48.png)

![pic-49](49.png)

You can insert multiple rows in a single command:
![pic-50](50.png)

It is also possible to insert the result of a query (which might be no rows, one row, or many rows):

![pic-51](51.png)

>**TiP:** When inserting a lot of data at the same time, consider using the COPY command. It is not as flexible as the INSERT command, but is more efficient.

