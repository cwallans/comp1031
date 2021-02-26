# comp1031

Graph Database Exercise:

Download the free Neo4j Community Edition from the Neo4j download website. They provide installers for Windows, Mac and Linux and a helpful desktop application.

When you run this application it will allow you to select a directory containing Neo4j data files. You can choose the graph-small directory from unpacking the zip file in order to access the IMDb example database. You can also leave it as the default, which will give you an empty database in which you can run through a tutorial.

To access the graphical interface, first start up the Neo4j database, and then point your web browser at localhost:7474. We suggest that you first do this with the default empty database, and follow some of the built-in tutorials available in the browser or desktop application.

Please use the Cypher query language to solve each of the following exercises.

Exercise 1:

This query:

    match (p1:Person)-[:ACTS_IN]->(:Movie)<-[:ACTS_IN]-(p2:Person)
    where p1.name = 'Lawrence, Jennifer (III)'
    and p2.name <> 'Lawrence, Jennifer (III)'
    return count(*) as total ;
returns a total of 331, while this query:

    match (p1:Person)-[:ACTS_IN]->(:Movie)<-[:ACTS_IN]-(p2:Person)
    where p1.name = 'Lawrence, Jennifer (III)'
    and p2.name <> 'Lawrence, Jennifer (III)'
    return count(distinct p2) as total ;

returns a total of 321. That is because some co-stars are counted twice in the first query and only once (correctly) in the second query. Who are the co-stars counted multiple times and how many movies did they act in with Jennifer Lawrence? Let's use Cypher to find out!

Complete the following Cypher query so that it returns rows name, total where the name column is the name of an actor, and the total column indicates the number of movies in which they co-starred with Jennifer Lawrence. Note, here we want the total to always be greater than 1. (HINT: Consider using the WITH construct.)

    YOUR-CODE-GOES-HERE
    return name, total
    order by name, total;
   
   
Exercise 2:

The distance between two actors A and B is 1 if they co-starred in the same movie; the distance is 2 if there is some other actor X such that A co-starred with X on some movie and X co-starred with B on some other movie; and so on.

For this exercise we will compute the distance between all of our genres. The definition of distance is similar: for example, the distance between two genres is 1 if there is at least one movie that is associated with those two genres. We can use this distance as a measure of how similar two genres are.

We will use the HAS_GENRE relationship rather than the ACTS_IN relationship. Your query should output the distance between every genre and every other genre that exists in the database. Make sure your query enforces the constraint g1.genre < g2.genre so that each pair of genres is only listed once (if you swap the order of the two genres, the distance is still the same).

    match (g:Genre)
    with g.genre as genre1
      YOUR-CODE-GOES-HERE
    return distinct genre1, g2.genre as genre2, length(path)/2 as length
    order by length desc, genre1, genre2;


Exercise 3:

Let's build a simple recommendation engine. Starting from a known movie that you liked, write a query to finds similar movies that you might also enjoy.

Let A be the movie that you liked. Some other movie B should be considered for recommendation if A and B have at least one genre in common, at least one keyword in common, and at least one actor in common. Furthermore, you can calculate a similarity score as follows: 1 point for every keyword that A and B have in common, and 10 points for every actor the movies have in common.

Write a query that produces recommendations for someone who liked Skyfall (2012). The results should give the title of each recommended movie and the similarity score, and be sorted by score:

    match
      YOUR-CODE-GOES-HERE
    return title, score
    order by score desc;
