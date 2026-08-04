Like most other relational database products, PostgreSQL supports *aggregate functions*. An aggregate function computes a single result from multiple input rows. For example, there are aggregates to compute the `count`, `sum`, `avg` (average), `max` (maximum) and `min` (minimum) over a set of rows.

![pic-21](21.png)

![pic-22](22.png)

Aggregates are also very useful in combination with `GROUP BY` clauses. For example, we can get the number of readings and the maximum low temperature observed in each city with:

![pic-23](23.png)

Result:

![pic-25](25.png)

which gives us one output row per city. Each aggregate result is computed over the table rows matching that city. We can filter these grouped rows using `HAVING`:

![pic-26](26.png)

Result:

![pic-27](27.png)

which gives us the same results for only the cities that have all temp_lo values below 40. Finally, if we only care about cities whose names begin with “S”, we might do:

![pic-28](28.png)

Result:

![pic-29](29.png)

