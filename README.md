#### Album-and-Track-Data-Analysis




### Table of Contents

- [Project Overview](project-overview)

- [Queries and Results](queries-and-results)

1. [Fetching Album Titles with Track Counts](fetching-album-titles-with-track-counts)
2. [Fetching the Track with the Highest Duration](fetching-the-track-with-the-highest-duration)
3. [Calculating Total Duration for Each Album](calculating-total-duration-for-each-album)
4. [Deleting Tracks Based on Conditions](deleting-tracks-based-0n-conditions)
5. [Updating Track Duration for Specific Track Numbers](updating-track-duration-for-specific-track-numbers)

- [Screenshots of Queries and Results](screenshots-of-queries-and-results)
  
- [Conclusion](conclusion)


## Project Overview

The dataset consists of two tables:

- Album Table: Contains information about music albums, with a primary key column named id.

- Track Table: Stores individual track details, where each track is associated with an album through the foreign key album_id.

# The goal of this project was to:

- Analyze and extract key information such as album titles, track counts, and track durations.

- Perform data cleaning by deleting unwanted records and updating certain values based on specific conditions.

## Queries and Results

1. Fetching Album Titles with Track Counts
I wrote an SQL query to list all album titles and the total number of tracks for each album, using a LEFT JOIN to link the album and track tables on the album_id. I used aliasing to make the result more readable, naming the columns Album_Title and Track_Count.

SQL Query:

sql

SELECT a.title AS Album_Title, COUNT(t.id) AS Track_Count 
FROM album a 
LEFT JOIN track t ON a.id = t.album_id 
GROUP BY a.id, a.title;

Explanation:

LEFT JOIN: Ensures all albums are listed, even those without any associated tracks.
GROUP BY: Groups the result by album id and title to aggregate the track count.

2. Fetching the Track with the Highest Duration
To identify the track with the longest duration, I used a subquery to find the maximum duration and retrieved the corresponding track title.

SQL Query:

sql
SELECT title 
FROM track 
WHERE duration = (SELECT MAX(duration) FROM track);

Explanation:

Subquery: Finds the maximum track duration from the track table.
WHERE clause: Matches the track with the highest duration.

3. Calculating Total Duration for Each Album
To calculate the total duration of tracks for each album, I aggregated the duration from the track table and joined it with the album table.

SQL Query:

sql
SELECT a.title AS Album_Title, SUM(t.duration) AS Total_Duration 
FROM album a 
LEFT JOIN track t ON a.id = t.album_id 
GROUP BY a.id, a.title;

Explanation:

SUM: Aggregates the total track duration for each album.
GROUP BY: Groups the results by album id and title.

4. Deleting Tracks Based on Conditions
I cleaned the data by deleting tracks that belonged to albums with album_id 1 and 11 and had a track_number between 6 and 8.

SQL Query:

sql
DELETE FROM track 
WHERE album_id IN (1, 11) AND track_number BETWEEN 6 AND 8;

Explanation:

IN clause: Filters the records where album_id is either 1 or 11.
BETWEEN: Selects tracks where the track_number is between 6 and 8 (inclusive).
Note:
If your SQL environment runs in safe update mode, you may encounter an error while executing DELETE queries. To temporarily disable safe mode, use:

sql
SET SQL_SAFE_UPDATES = 0;
After completing the operation, re-enable it:

sql
SET SQL_SAFE_UPDATES = 1;

5. Updating Track Duration for Specific Track Numbers
I updated the duration of all tracks with a track_number below 4 to 1050.

SQL Query:

sql
UPDATE track 
SET duration = 1050 
WHERE track_number < 4;

Explanation:

WHERE clause: Ensures only tracks with a track_number below 4 are updated.
To verify the changes, I used the following query:

sql
SELECT * FROM track WHERE track_number < 4;
Note:
Similar to the delete query, if safe update mode is enabled, use the following to disable it:

sql
SET SQL_SAFE_UPDATES = 0;
After completing the update, re-enable safe mode:

sql
SET SQL_SAFE_UPDATES = 1;

## Screenshots of Queries and Results

Below are the screenshots of the queries executed and their results, showcasing the steps taken and the outcomes achieved throughout the project.


![Delete Track](https://github.com/user-attachments/assets/f6188c38-5628-41bd-b401-ed2e78cd2535)
![Highest duration](https://github.com/user-attachments/assets/b354a832-b0fd-4006-8171-9dedb7ff0edb)
![Album Table](https://github.com/user-attachments/assets/3a8bf18d-7d2b-4b76-80b4-e5d6acf5e7c6)
![Track Table](https://github.com/user-attachments/assets/9f3ebd53-bb3b-4091-9d81-d8ccfabd804b)
![Select Update](https://github.com/user-attachments/assets/f331c2ef-bff3-48c6-95d0-0f153e46a996)
![Total Duration](https://github.com/user-attachments/assets/fd549fd9-f069-45c1-a9f7-ef6fc17bda6b)
![Track Count](https://github.com/user-attachments/assets/a8d71659-b7d1-4584-966c-c00f78745c43)
![Track Update](https://github.com/user-attachments/assets/0b0f2e44-a5dc-4182-9e52-7a6c2acd4f74)








## Conclusion
This project gave me practical experience with SQL querying and data manipulation. I successfully used joins, aggregate functions, subqueries, and conditional statements to extract insights and perform updates on the data. Additionally, I implemented data cleaning techniques by deleting unnecessary records based on specific conditions.

Through this project, I enhanced my skills in:

- Writing optimized SQL queries.

- Performing data aggregation and analysis.

- Handling database constraints like safe update mode.

This project demonstrates my ability to analyze data, clean it, and manage databases efficiently, providing value in a professional data environment.
