### SQL Lesson 1: `SELECT queries 101`

1. Find the title of each film.  
    - `SELECT Title FROM movies;`
2. Find the director of each film
    - `SELECT Director FROM movies;`
3. Find the title and director of each film
    - `SELECT Title, Director FROM movies;`
4. Find the title and year of each film
    - `SELECT Title, Year FROM movies;`
5. Find all the information about each film
    - `SELECT * FROM movies;`

### SQL Lesson 2: `Queries with constraints (Pt. 1)`

1. Find the movie with a row id of 6
    - `SELECT * FROM movies where id=6;`
2. Find the movies released in the years between 2000 and 2010
    - `SELECT * FROM movies where year between 2000 and 2010;`
3. Find the movies not released in the years between 2000 and 2010
    - `SELECT * FROM movies where year not between 2000 and 2010;`
4. Find the first 5 Pixar movies and their release year
    - `SELECT * FROM movies where id between 1 and 5;` or
    - `SELECT * FROM movies where id <=5;`

### SQL Lesson 3: `Queries with constraints (Pt. 2)`

1. Find all the Toy Story movies
    - `SELECT * FROM movies where title like "%toy story%";`
2. Find all the movies directed by John Lasseter
    - `SELECT * FROM movies where director like "%john lasseter%";`
3. Find all the movies (and director) not directed by John Lasseter
    - `SELECT * FROM movies where director not like "%john lasseter%";`
4. Find all the WALL-* movies
    - `SELECT * FROM movies where title like "%wall-%";

### SQL Lesson 4: `Filtering and sorting Query results`

1. List all directors of Pixar movies (alphabetically), without duplicates
    - `SELECT distinct director FROM movies order by director asc ;`
2. List the last four Pixar movies released (ordered from most recent to least)
    - `SELECT distinct title FROM movies order by year desc limit 4 ;`
3. List the first five Pixar movies sorted alphabetically
    - `SELECT distinct title FROM movies order by title asc limit 5 ;`
4. List the next five Pixar movies sorted alphabetically
    - `SELECT distinct title FROM movies order by title asc limit 5 offset 5 ;`

### SQL Review: `Simple SELECT Queries`

1. List all the Canadian cities and their populations
    - `SELECT city,population FROM north_american_cities where country like "%canada%";`
2. Order all the cities in the United States by their latitude from north to south
    - `SELECT * FROM north_american_cities where country = "United States" order by latitude desc;`
3. List all the cities west of Chicago, ordered from west to east
    - `SELECT * FROM north_american_cities where longitude < -87.629798 order by longitude;`
4. List the two largest cities in Mexico (by population)
    - `SELECT * FROM north_american_cities where country="Mexico" order by population desc limit 2;`
5. List the third and fourth largest cities (by population) in the United States and their population
    - `SELECT * FROM north_american_cities where country="United States" order by population desc limit 2 offset 2;`

### SQL Lesson 6: `Multi-table queries with JOINs`

1. Find the domestic and international sales for each movie
    - `SELECT * FROM movies inner join Boxoffice on id = movie_id;`
2. Show the sales numbers for each movie that did better internationally rather than domestically
    - `SELECT * FROM movies inner join Boxoffice on id = movie_id where International_sales > Domestic_sales;`
3. List all the movies by their ratings in descending order
    - `SELECT * FROM movies inner join Boxoffice on id =movie_id order by rating desc ;`

### SQL Lesson 7: `OUTER JOINs`

1. Find the list of all buildings that have employees
    - `SELECT distinct Building FROM employees;`
2. Find the list of all buildings and their capacity
    - `SELECT * FROM Buildings ;`
3. List all buildings and the distinct employee roles in each building (including empty buildings)
    - `SELECT distinct Building_name,role FROM Buildings left join Employees on Building_name = Building ;`

### SQL Lesson 8: `A short note on NULLs`

1. Find the name and role of all employees who have not been assigned to a building
    - `SELECT name,role FROM employees where Building is null; `
2. Find the names of the buildings that hold no employees
    - `SELECT * FROM Buildings left join Employees on Building_name=Building where role is null; `

### SQL Lesson 9: `Queries with expressions`

1. List all movies and their combined sales in millions of dollars ✓
    - `SELECT *,(Domestic_sales+International_sales)/1000000 as total_sales FROM movies inner join Boxoffice on id = Movie_id;`
2. List all movies and their ratings in percent
    - `SELECT *,(rating*10) as percent FROM movies inner join Boxoffice on id = Movie_id;
3. List all movies that were released on even number years
    - `SELECT * FROM movies where year % 2 = 0;`

### SQL Lesson 10: `Queries with aggregates (Pt. 1)`

1. Find the longest time that an employee has been at the studio
    - `SELECT *,max(Years_employed) FROM employees;`
2. For each role, find the average number of years employed by employees in that role
    - `SELECT *,avg(Years_employed) FROM employees group by role;`
3. Find the total number of employee years worked in each building
    - `SELECT *,sum(Years_employed) FROM employees group by building;`

### SQL Lesson 11: `Queries with aggregates (Pt. 2)`

1. Find the number of Artists in the studio (without a HAVING clause)
    - `SELECT *,count(role) FROM employees where role = "Artist";`
2. Find the number of Employees of each role in the studio
    - `SELECT *,count(role) FROM employees group by role;`
3. Find the total number of years employed by all Engineers
    - `SELECT *,sum(years_employed) FROM employees where role = "Engineer";`

### SQL Lesson 12: `Order of execution of a Query`

1. Find the number of movies each director has directed    - ``

    - `SELECT *,count(Director) FROM movies group by Director;`
2. Find the total domestic and international sales that can be attributed to each director
    - `SELECT *,sum(Domestic_sales+International_sales) FROM movies inner join Boxoffice on id = movie_id group by director;`

### SQL Lesson 13: `Inserting rows`

1. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)
    - `INSERT INTO movies values (4,"Toy Story 4","	John Lasseter",2023,120);`
2. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table.
    - `insert into Boxoffice values(4,8.7,340000000,270000000);`

### SQL Lesson 14: `Updating rows`

1. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter
    - `update movies set Director="John Lasseter" where id = 2 ;`
2. The year that Toy Story 2 was released is incorrect, it was actually released in 1999
    - `update movies set year = 1999 where title = "Toy Story 2" ;`
3. Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich
    - `update movies set title = "Toy Story 3", Director = "Lee Unkrich" where title = "Toy Story 8"`

### SQL Lesson 15: `Deleting rows`

1. This database is getting too big, lets remove all movies that were released before 2005.
    - `delete FROM movies where year < 2005;`
2. Andrew Stanton has also left the studio, so please remove all movies directed by him.
    - `delete from movies where Director = "Andrew Stanton";`

### SQL Lesson 16: `Creating tables`

1. Create a new table named Database with the following columns:
– Name A string (text) describing the name of the database
– Version A number (floating point) of the latest version of this database
– Download_count An integer count of the number of times this database was downloaded
    - `create table database (Name text,version float,Download_count integer);`

### SQL Lesson 17: `Altering tables`

1. Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in.
    - `alter table movies add Aspect_ratio float;`
2. Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English.
    - `alter table movies add language text default english;`

### SQL Lesson 18: `Dropping tables`

1. We've sadly reached the end of our lessons, lets clean up by removing the Movies table
    - `drop table if exists movies;`
2. And drop the BoxOffice table as well
    - `drop table if exists boxoffice;`

    