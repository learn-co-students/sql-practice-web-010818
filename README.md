# Intro to SQL

1. Install the SQLite Browser if you haven't already [here](http://sqlitebrowser.org/)
2. Open the SQLite Browser and click 'File -> Open DataBase'
3. Choose the `chinook.db` file from this repo. This database is open source and maintained by Microsoft (SQL is no fun if you don't have any data)


## WHAT are the 4 things I can do to data?





## Challenges

1. How would you return all of the rows in the artists table?
  ```SQL
  "SELECT * FROM artist;"

  ```
2. How would you select the artist with the name "Black Sabbath"
  ```SQL
  "SELECT * FROM artist WHERE name='Black Sabbath';"

  ```
3. How would you create a table named 'fans' with an autoincrementing ID that's a primary key and a name field of type text

"CREATE TABLE fans (
  id INTEGER PRIMARY KEY,
  name TEXT
  );"


4. How would you alter the fans table to have a artist_id column type integer?
ALTER TABLE fans ADD_COLUMN artist_id INTEGER;
  ""
5. How would you add yourself as a fan of the Black Eyed Peas?
  ```sql


  INSERT INTO fans (name, artist_id) VALUES ("Josh", 169) WHERE artist.id = fans.artist_id;
  ```


6. How would you return fans that are not fans of the black eyed peas.
  ```sql
  SELECT * FROM fans where NOT id = 169;

  ```
7. Display an artists name next to their album title

  SELECT artist.name, album.title * FROM artists JOIN artists BY artists.id=albums.artistId
```sql


SELECT artists.name, albums,title FROM artists INNER JOIN albums ON a.artistid = albums.artistid ORDERBY arist.name

```

8. Display artist name, album name and number of tracks on that album
```sql

SELECT artists.name, albums,title, tracks.albumid FROM artists INNER JOIN albums ON a.artistid = albums.artistid
JOIN tracks ON tracks.albumid = albums.albumsid GROUP BY arists.name


```

9.  How would you return the name of all of the artists in the 'Pop' Genre
  ```sql

  SELECT artists.name FROM artists
 INNER JOIN albums ON artists.artistid = albums.artistid /* adding artists and album(goes_first) table where it is applied */
 INNER JOIN tracks ON albums.albumid = tracks.albumid
 INNER JOIN genres ON tracks.genreid = genres.genreid
 WHERE genres.name ='Pop' GROUP BY artists.name;





10. I want to return the names of the artists and their number of rock tracks
 who play Rock music
and have move than 30 tracks
in order of the number of rock tracks that they have
from greatest to least


SELECT artists.name, COUNT(tracks.name) AS count FROM artists
INNER JOIN albums ON artists.artistid = albums.artistid /* adding artists and album(goes_first) table where it is applied */
INNER JOIN tracks ON albums.albumid = tracks.albumid
INNER JOIN genres ON tracks.genreid = genres.genreid
GROUP BY artists.name HAVING genres.name='Rock' AND count > 30
ORDER BY count DESC;
