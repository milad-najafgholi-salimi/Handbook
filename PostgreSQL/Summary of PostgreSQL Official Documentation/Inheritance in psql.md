Inheritance is a concept from object-oriented databases. It opens up interesting new possibilities of database design.

Let's create two tables: A table cities and a table capitals. Naturally, capitals are also cities, so you want some way to show the capitals implicitly when you list all cities. If you're really clever you might invent some scheme like this:

![pic-38](38.png)

This works OK as far as querying goes, but it gets ugly when you need to update several rows, for one thing.

A better solution is this:

![pic-39](39.png)

For example, the following query finds the names of all cities, including state capitals, that are located at an elevation over 500 feet:
![pic-40](40.png)

which returns:
![pic-41](41.png)

On the other hand, the following query finds all the cities that are not state capitals and are situated at an elevation over 500 feet:
![pic-42](42.png)

Here the ONLY before cities indicates that the query should be run over only the cities table, and not tables below cities in the inheritance hierarchy. Many of the commands that we have already discussed — SELECT, UPDATE, and DELETE — support this ONLY notation.
