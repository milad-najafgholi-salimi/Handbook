Rows can be removed from a table using the `DELETE` command. Suppose you are no longer interested in the weather of Hayward. Then you can do the following to delete those rows from the table:

![pic-32](32.png)

All weather records belonging to Hayward are removed.

---
One should be wary of statements of the form

![pic-33](33.png)

Without a qualification, `DELETE` will remove all rows from the given table, leaving it empty. The system will not request confirmation before doing this!

