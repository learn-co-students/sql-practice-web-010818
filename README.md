# Intro to SQL

1. Install the SQLite Browser if you haven't already [here](http://sqlitebrowser.org/)
2. Open the SQLite Browser and click 'File -> Open DataBase'
3. Choose the `chinook.db` file from this repo. This database is open source and maintained by Microsoft (SQL is no fun if you don't have any data)


## WHAT are the 4 things I can do to data?





## Challenges

1. How would you return all of the rows in the artists table?
  ```SQL
SELECT * FROM artists;
  ```
2. How would you select the artist with the name "Black Sabbath"
  ```SQL
SELECT * FROM artists WHERE artists.name = "Black Sabbath";
  ```
3. How would you create a table named 'fans' with an autoincrementing ID that's a primary key and a name field of type text

  ```sql
CREATE TABLE fans (id INTEGER PRIMARY KEY, name TEXT);
  ```

4. How would you alter the fans table to have a artist_id column type integer?
ALTER TABLE fans ADD COLUMN artist_id INTEGER;
  ```sql
ALTER TABLE fans ADD COLUMN artist_id INTEGER;
  ```
5. How would you add yourself as a fan of the Black Eyed Peas?
  ```sql

INSERT INTO fans (name, artist_id) VALUES ('TORRE', 169);

-- INSERT INTO fans (name, artist_id) VALUES ('Torre', NULL);
-- UPDATE fans
-- SET fans.artist_id = artists.artistid
-- FROM fans
-- INNER JOIN artists ON artists.artistid = fans.artist_id
-- WHERE fans.artist_id IS NULL and artists.name = 'Black Eyed Peas';
--
-- SELECT artists.artistid AS ID
-- FROM artists
-- WHERE artists.name = 'Black Eyed Peas';
-- INSERT INTO fans (name, artist_id)
-- VALUES ('Torre', ID);
  ```

6. How would you return fans that are not fans of the black eyed peas.
  ```sql
SELECT fans.id, fans.name
FROM fans
INNER JOIN artists ON fans.artist_id = artists.artistid
WHERE artists.name != 'Black Eyed Peas';
  ```
7. Display an artists name next to their album title
```sql
SELECT artists.name, albums.title
FROM artists
INNER JOIN albums ON artists.artistid = albums.artistid
ORDER BY(artists.name);
```

8. Display artist name, album name and number of tracks on that album
```sql
SELECT artists.name, albums.title, COUNT(tracks.albumid)
FROM artists
INNER JOIN albums ON albums.artistid = artists.artistid
INNER JOIN tracks ON albums.albumid = tracks.albumid
WHERE tracks.albumid = albums.albumid and albums.artistid = artists.artistid
GROUP BY artists.name;
```

9.  How would you return the name of all of the artists in the 'Pop' Genre
  ```sql
SELECT artists.name
FROM artists
INNER JOIN albums ON albums.artistid = artists.artistid
INNER JOIN tracks ON albums.albumid = tracks.albumid
INNER JOIN genres ON genres.genreid = tracks.genreid
WHERE genres.name = 'Pop'
GROUP BY(artists.name);

  ```


10. I want to return the names of the artists and their number of rock tracks
 who play Rock music
and have move than 30 tracks
in order of the number of rock tracks that they have
from greatest to least

```sql
SELECT artists.name, COUNT(tracks.genreid) AS 'Rock Tracks'
FROM artists
INNER JOIN albums ON albums.artistid = artists.artistid
INNER JOIN tracks ON albums.albumid = tracks.albumid
INNER JOIN genres ON genres.genreid = tracks.genreid
GROUP BY(artists.name)
HAVING COUNT(tracks.genreid) > 30 and genres.name = 'Rock'
ORDER BY(COUNT(tracks.genreid)) DESC;
```
