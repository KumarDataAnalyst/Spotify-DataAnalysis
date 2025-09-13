# Spotify-DataAnalysis

# Features

* Fetch metadata (track name, artist, album, popularity, duration) from Spotify API.

* Insert track data into a MySQL database (spotify_db).

* Process multiple Spotify track URLs in bulk from track_urls.txt.

* Save data into CSV for offline use.

* Perform SQL queries:

  - Find most popular track.

  - Calculate average popularity.

  - Filter tracks longer than 4 minutes.

  - Categorize tracks into popularity ranges.

  - Visualize track features (popularity & duration) using Matplotlib.
 

 # Jupyter Notebook
 
  Using %sql Magic (easier for SQL only)

     --Load SQL extension
         %load_ext sql

      --Connect to MySQL
         %sql mysql+mysqlconnector://root:root@localhost/spotify_db


  (replace root:root with your username & password)


# Requirements & Dependencies

* Python 3.8+

* MySQL Server 

# Python libraries:

* Install dependencies with:

       pip install spotipy mysql-connector-python pandas matplotlib


# Configure Spotify API credentials

* Go to Spotify Developer Dashboard

* Create an app → get Client ID and Client Secret.

* Replace them in the scripts (spotify.py, spotify_mysql.py, spotify_mysql_urls.py):

           sp = spotipy.Spotify(auth_manager=SpotifyClientCredentials(
           client_id="YOUR_CLIENT_ID",
           client_secret="YOUR_CLIENT_SECRET"
           ))

# Configure MySQL

Start MySQL server

Run the schema script:

    source spotify.sql;

This will create:

Database: spotify_db

Table: spotify_tracks

Update your MySQL credentials inside the Python scripts:

     db_config = {
    'host': 'localhost',
    'user': 'root',
    'password': 'yourpassword',
    'database': 'spotify_db'
     }

     Insert multiple tracks from a file

# Insert multiple tracks from a file

Add track URLs to track_urls.txt.

Run:

python spotify_mysql_urls.py


* Fetches and inserts all listed tracks into MySQL.

# SQL Analysis

Open MySQL shell and run:

    USE spotify_db;

    -- Most popular track
     SELECT track_name, artist, album, popularity
     FROM spotify_tracks
     ORDER BY popularity DESC
     LIMIT 1;

     -- Average popularity
     SELECT AVG(popularity) AS average_popularity FROM spotify_tracks;

     -- Tracks longer than 4 minutes
     SELECT track_name, artist, duration_minutes
     FROM spotify_tracks
     WHERE duration_minutes > 4.0;

     -- Categorize tracks by popularity
     SELECT 
       CASE 
          WHEN popularity >= 80 THEN 'Very Popular'
          WHEN popularity >= 50 THEN 'Popular'
          ELSE 'Less Popular'
      END AS popularity_range,
      COUNT(*) AS track_count
    FROM spotify_tracks
    GROUP BY popularity_range;

  # Example Output

  CSV file: spotify_track_data.csv

  Visualization: Bar chart of track popularity & duration.

  Database: Populated spotify_tracks table.

# Acknowledgements

   Spotify Web API

   Spotipy library




