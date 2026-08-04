Sometimes it is useful to obtain data from modified rows while they are being manipulated. The `INSERT`, `UPDATE`, `DELETE`, and `MERGE` commands all have an optional `RETURNING` clause that supports this. Use of `RETURNING` avoids performing an extra database query to collect the data, and is especially valuable when it would otherwise be difficult to identify the modified rows reliably.

![pic-57](57.png)

![pic-58](58.png)

The `RETURNING` clause is also very useful with `INSERT` ... `SELECT`.

In an `UPDATE`, the default data available to `RETURNING` is the new content of the modified row. For example:

![pic-59](59.png)

In a `DELETE`, the default data available to `RETURNING` is the content of the deleted row. For example:

![pic-60](60.png)

In a `MERGE`, the default data available to `RETURNING` is the content of the source row plus the content of the inserted, updated, or deleted target row. Since it is quite common for the source and target to have many of the same columns, specifying `RETURNING` `*` can lead to a lot of duplicated columns, so it is often more useful to qualify it so as to return just the source or target row. For example:

![pic-61](61.png)

In each of these commands, it is also possible to explicitly return the old and new content of the modified row. For example:

![pic-62](62.png)

In this example, writing `new.price` is the same as just writing `price`, but it makes the meaning clearer.