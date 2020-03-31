# Project Description
Define fact and dimension tables for a star schema for a particular analytic focus, and write an ETL pipeline that transfers data from files in two local directories into tables in Postgres.

# Purpose
Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app.

# Sparkify goals
* Understanding what songs users are listening to.
* Postgres database with tables designed to optimize queries on song play analysis.
* Easy way to query their data.

# Database schema
The database has a star schema composed by one fact table called songplays and four dimensional tables (users, songs, artists, time).
The benefits of the schema are:
* Query performance
* Because a star schema database has a small number of tables and clear join paths, queries run faster.
* Load performance and administration
* Structural simplicity also reduces the time required to load large batches of data into a star schema database. 
* Easily understood

**Fact Table**
*songplays* - records in log data associated with song plays i.e. records with page NextSong
fields: songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

**Dimension Tables**
*users* - users in the app. 
fields: user_id, first_name, last_name, gender, level
*songs* - songs in music database
fields: song_id, title, artist_id, year, duration
*artists* - artists in music database
fields: artist_id, name, location, latitude, longitude
*time* - timestamps of records in songplays broken down into specific units
fields: start_time, hour, day, week, month, year, weekday

# ETL pipeline
* 1- Conection to the database.
* 2- Get all the files from song_data.
* 3- For each file a DataFrame is created with the desired fields.
* 4- Insert the rows into songs table and artist table.
* 5- Get all the files from log_data.
* 6- For each log file:
    * Filter by NextSong action
    * Convert timestamp column to datetime
    * Insert time data records
    * Create users table
    * Inster users table
    * Get songid and artistid from song and artist tables
    * Insert songplay record

# Files description.
**create_tables.py** - Script for creating the database and tables.

**sql_queries.py** - Script that contains the needed instructions to drop and craeate tables. Also to insert rows and needed queries.

**etl.py** - Script that fetch the data from the different folders and create the data pipelines to transform and load the data
into our Postgres DataBase.

**etl.ipynb** - Notebook for prototyping our data pipelines.

**test.ipynb** - Notebook for testing purposes.

# How to run the Python scripts
In your terminal:
* 1- Execute create_tables.py using: python create_tables.py
* 2- Execute etl.py: python etl.py

