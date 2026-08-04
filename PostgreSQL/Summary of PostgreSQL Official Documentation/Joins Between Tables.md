Queries that access multiple tables (or multiple instances of the same table) at one time are called `join` queries. They combine rows from one table with rows from a second table, with an expression specifying which rows are to be paired. For example, to return all the weather records together with the location of the associated city, the database needs to compare the `city` column of each row of the `weather` table with the `name` column of all rows in the `cities` table, and select the pairs of rows where these values match.3 This would be accomplished by the following query:

![pic-18](18.png)

Second table columns will be appended at the end.

![pic-19](19.png)

Since the columns all had different names, the parser automatically found which table they belong to. If there were duplicate column names in the two tables you'd need to `qualify` the column names to show which one you meant, as in:

![pic-20](20.png)

