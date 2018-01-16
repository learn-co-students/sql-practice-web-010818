# Intro to SQL

1. Install the SQLite Browser if you haven't already [here](http://sqlitebrowser.org/)
2. Open the SQLite Browser and click 'File -> Open DataBase'
3. Choose the `chinook.db` file from this repo. This database is open source and maintained by Microsoft (SQL is no fun if you don't have any data)


## WHAT are the 4 things I can do to data?





## Challenges

1. How would you return all of the rows in the artists table?
  ```SQL
  SELECT* artist FROM artists
  ```
2. How would you select the artist with the name "Black Sabbath"
  ```SQL
  SELECT* artist.name FROM artists WHERE artist.name="Black Sabbath"
  ```
3. How would you create a table named 'fans' with an autoincrementing ID that's a primary key and a name field of type text

  ```sql
  CREATE TABLE fans (id INTEGER PRIMARY KEY, name TEXT)
  ```

4. How would you alter the fans table to have a artist_id column type integer?

  ```sql
  ALTER TABLE fans ADD COLUMN artist_id INTEGER
  ```
5. How would you add yourself as a fan of the Black Eyed Peas?
  ```sql
  SELECT artists.artistid
  FROM artist
  WHERE artist.name="Black Eyed Peas"
  INSERT INTO fans(name, artist_id)
  VALUES ("Declan",169)
  ```


6. How would you return fans that are not fans of the black eyed peas.
  ```sql
  SELECT* FROM fans WHERE artist_id!=169

  SELECT* FROM fans INNER JOIN artists ON fans.artist_id = artists.ArtistId
  WHERE artists.name!="Black Eyed Peas"
  ```
7. Display an artists name next to their album title
```sql
  SELECT artists.name, album.title FROM artists INNER JOIN albums ON artist.ArtistId = albums.ArtistId,
  ORDER BY artist.Name
```

8. Display artist name, album name and number of tracks on that album
```sql
  SELECT artists.name, album.title, COUNT(tracks.albumid)
  FROM artists INNER JOIN albums ON artists.artistid = albums.artistid
  INNER JOIN tracks ON albums.albumid = tracks.albumid
  WHERE artist.artistid=albums.artistid AND albums.albumid=tracks.albumid
  GROUP BY artist.name
```

9.  How would you return the name of all of the artists in the 'Pop' Genre
  ```sql
  SELECT artists.name
  FROM artists
  INNER JOIN albums ON artists.artistid=albums.ArtistId
  INNER JOIN tracks ON albums.albumid=tracks.albumid
  INNER JOIN genres ON tracks.genreid=genres.genreid
  WHERE genres.name="Pop"
  GROUP BY artists.name

  ```


10. I want to return the names of the artists and their number of rock tracks
 who play Rock music
and have move than 30 tracks
in order of the number of rock tracks that they have
from greatest to least

```sql
  SELECT artists.name, COUNT(tracks.genreid) AS "Rock Tracks"
  FROM artists
  INNER JOIN albums ON artists.artistid=albums.artistid
  INNER JOIN tracks ON albums.albumid=tracks.albumid
  INNER JOIN genres ON tracks.genreid=genres.genreid
  GROUP BY artists.name
  Having(COUNT(tracks.genreid)>30) AND genres.name="Rock"
  ORDER BY COUNT(tracks.name) DESC

```
