  * List all the films that were made in 2004

  ```
  SELECT * FROM films WHERE year = 2004;
  ```

  * List all the films  with a duration of 100 minutes or greater

  ```  
  SELECT * FROM films WHERE duration >= 100;
  ```

  * List these films in order, from the longest to the shortest

  ```
  SELECT * FROM films WHERE duration >= 100 ORDER by duration DESC;
  ```

  * List all the films that have a title that contains the word 'the'

  ```
  SELECT * FROM films WHERE title LIKE '%the%';
  ```

  * List all the films that have a title that starts with the word 'the'

  ```
  SELECT * FROM films WHERE title LIKE 'The%';
  ```

  * List all the films that have a title that contains the word 'the' that weren't made in 2004

  ```
  SELECT * FROM films WHERE title LIKE '%the%' AND year <> 2004;
  ```

  * List all the films except for 'Mean Girls' and 'Get Out' that have a title that contains the letter 'g'

  ```
  SELECT * FROM films WHERE title LIKE '%g%' AND title NOT IN("Mean Girls","Get Out");
  ```

  * List the three shortest films

  ```
  SELECT * FROM films ORDER BY duration ASC LIMIT 3;
  ```

  * List the 4th and 5th oldest films

  ```
  SELECT * FROM films ORDER BY year LIMIT 2 OFFSET 3;
  ```

  * List the total duration of all the films in the table

  ```
  SELECT SUM(duration) AS 'Total Duration' FROM films;
  ```

  * List all the different years (no duplicates) in the table

  ```
  SELECT DISTINCT(year) FROM films ORDER by year ASC;
  ```

  * Display the number of films in the table

  ```
  SELECT COUNT(*) AS 'Number of Films' FROM films;
  ```

  * Display the average duration of all the films in the database

  ```
  SELECT AVG(duration) AS 'Average Duration' FROM films;
  ```

  * Display the average duration of all the films made in the 21st century

  ```
  SELECT AVG(duration) AS 'Average Duration' FROM films WHERE year >=2000;
  ```

  * List each year and the number of films made in that year

  ```
  SELECT year, COUNT(year) as "No. Films" FROM  films GROUP BY year;
  ```

  * List each year. For each year, display the average duration of all the films made in that year, order the results in ascending order

  ```
  SELECT year, AVG(duration) as "Average Length" FROM  films GROUP BY year ORDER BY year ASC;
  ```
  
  * Modify the above by rounding the duration of each film to the nearest minute (you might have to do some extra research)

  ```
  SELECT year, ROUND(AVG(duration),0) as "Average Length" FROM  films GROUP BY year ORDER BY year ASC;
  ```
