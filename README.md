# Spring Boot with SpringData Neo4J
Users rate different movies (like IMDB). Hence Users will have RATED relationship on Movies.

## Version used
- Spring Boot - 1.5.14.RELEASE
- Neo4J Bolt Driver - 2.1.1

## REST endpoint
- `/rest/neo4j/user` - returns all users and their relationships (movies)

## Neo4J 
- Docker command to bring up Neo4J server
```
docker run --publish=7474:7474 --publish=7687:7687 neo4j:3.0
```
- Neo4J Browser URL
```
http://localhost:7474/browser
```

## Cypher Queries for Neo4J
- Creation of Movie and User nodes:

```
CREATE (Inception:Movie {title: 'Inception', director: 'Christopher Nolan'})
CREATE (DarkKnight:Movie {title: 'The Dark Knight', director: 'Christopher Nolan'})
CREATE (Peter:User {name: 'Peter N', age: 30})
CREATE (Sam:User {name: 'Sam Sheldon', age: 20})
CREATE (Ryan:User {name: 'Ryan A', age: 35})

CREATE
(Inception)-[:RATED {rating: 9}]->(Peter),
(Inception)-[:RATED {rating: 8}]->(Sam),
(DarkKnight)-[:RATED {rating: 9}]->(Sam),
(DarkKnight)-[:RATED {rating: 8}]->(Peter)

;
```
- Adding new relationship

```
MATCH (DarkKnight:Movie {title: 'The Dark Knight'}), (Ryan:User)
CREATE
(DarkKnight)-[:RATED {rating: 8}]->(Ryan)
;
```