# Intro to SQL

1. Install the SQLite Browser if you haven't already [here](http://sqlitebrowser.org/)
2. Open the SQLite Browser and click 'File -> Open DataBase'
3. Choose the `chinook.db` file from this repo. This database is open source and maintained by Microsoft (SQL is no fun if you don't have any data)


## WHAT are the 4 things I can do to data?





## Challenges

1. How would you return all of the rows in the artists table?
  ```sql
  SELECT * FROM artists;

  ```
2. How would you select the artist with the name "Black Sabbath"
  ```sql
  SELECT * FROM artists WHERE name='Black Sabbath';

  ```
3. How would you create a table named 'fans' with an autoincrementing ID that's a primary key and a name field of type text

  ```sql
  CREATE TABLE fans (id INTEGER PRIMARY KEY, name TEXT);

  ```

4. How would you alter the fans table to have a artist_id column type integer?

  ```sql
  ALTER TABLE fans ADD COLUMN artist_id INTEGER;

  ```
5. How would you add yourself as a fan of the Black Eyed Peas?
  ```sql
INSERT INTO fans (name, artist_id) SELECT "Matt", artists.ArtistId FROM artists WHERE artists.Name = "Black Eyed Peas";
  ```


6. How would you return fans that are not fans of the black eyed peas.
  ```sql
  SELECT * FROM fans
  INNER JOIN artists ON fans.artist_id = artists.ArtistId
  WHERE artists.Name != "Black Eyed Peas";

  ```
7. Display an artists name next to their album title
```sql
SELECT artists.name, albums.title FROM artists
INNER JOIN albums ON artists.ArtistId = albums.artistid;
```

8. Display artist name, album name and number of tracks on that album
```sql
SELECT artists.name, albums.title, COUNT(tracks.trackid) FROM artists
INNER JOIN albums ON artists.ArtistId = albums.ArtistId
INNER JOIN tracks ON albums.albumid = tracks.AlbumId
GROUP BY tracks.albumid;
```

9.  How would you return the name of all of the artists in the 'Pop' Genre
  ```sql
  SELECT distinct artists.Name FROM artists
  INNER JOIN tracks ON artists.ArtistId = tracks.AlbumId
  INNER JOIN albums ON tracks.AlbumId = albums.AlbumId
  INNER JOIN genres ON genres.GenreId = tracks.GenreId
  WHERE genres.Name = "Pop";

  ```


10. I want to return the names of the artists and their number of rock tracks
 who play Rock music
and have move than 30 tracks
in order of the number of rock tracks that they have
from greatest to least

```sql
SELECT artists.Name, COUNT(tracks.trackid) FROM artists
INNER JOIN tracks ON tracks.AlbumId = albums.AlbumId
INNER JOIN albums ON artists.ArtistId = albums.ArtistId
GROUP BY artists.artistid
HAVING COUNT(tracks.trackid) > 30
ORDER BY COUNT(tracks.trackid) DESC;
```
