The modification of data that is already in the database is referred to as updating. You can update individual rows, all the rows in a table, or a subset of all rows. Each column can be updated separately; the other columns are not affected.

To update existing rows, use the UPDATE command. This requires three pieces of information:
1. The name of the table and column to update
2. The new value of the column
3. Which row(s) to update

For example, this command updates all products that have a price of 5 to have a price of 10:

![pic-52](52.png)

This might cause zero, one, or many rows to be updated. It is not an error to attempt an update that does not match any rows.

![pic-53](53.png)

You can update more than one column in an UPDATE command by listing more than one assignment in the SET clause. For example:

![pic-54](54.png)

