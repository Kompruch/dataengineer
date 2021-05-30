# Sparkify ETL and Postgres Data Modeling

## The project

In this project we create Postgresql database and extract, transform, and load data into the database from json file for Sparkify. They'd like to create a Postgres database with tables designed to optimize queries on song play analysis.This database will allow Sparkify team to access and analyze data faster using SQL.

## The Schemas

There are four tables (songs, artist, time, user, and songplay).
songs, artist, time, and user tables are dimension tables which support songplay table which is fact table based on star schemas.
songplay table can be easily query to analyze user behavior when using our services.

the structure of each table are as follows:
* songs
    * songs table has 5 columns:
        * song_id TEXT PRIMARY KEY - This field contains song id for each song
        * title TEXT NOT NULL - This field contains title for each song
        * artist_id TEXT NOT NULL - This field contains artist id for each song
        * year INT - This field contains year for each song
        * duration NUMERIC - This field contains duration for each song
* artist
    * artist table has 5 colums:
        * artist_id TEXT PRIMARY KEY - This field contains artist id 
        * name TEXT NOT NULL - This field contains name 
        * location TEXT - This field contains location of artist 
        * latitude NUMERIC - This field contains latitude of artist
        * longitude NUMERIC - This field contains longitude of artist
* time
    * time table has 7 columns:
        * start_time TIMESTAMP PRIMARY KEY - This field contains start_time of each session
        * hour INT - This field contains hour 
        * day INT - This field contains day
        * week INT - This field contains week
        * month INT - This field contains month
        * year INT - This field contains year
        * weekday INT - This field contains weekday (start with monday = 0)
* user
    * user table has 5 columns:
        * user_id INT PRIMARY KEY - This field contains user id 
        * first_name TEXT NOT NULL - This field contains first name
        * last_name TEXT NOT NULL - This field contains last name
        * gender CHAR(1) - This field contains gender (M = male, F = female)
        * level TEXT) - The subscription level for user (free, or paid)
* songplay
    * songplay table: This table is a fact table that link to other dimension tables:
        * songplay_id SERIAL PRIMARY KEY - This field contains unique id for songplay
        * start_time TIMESTAMP - This contain timestamp for each session which is the FK from time table
        * user_id INT - This contain user id which is the FK from user table
        * level TEXT - The subscription level for user (free, or paid). it can be accessed easier
        * song_id TEXT - This contain song id which is the FK from song table
        * artist_id TEXT - This contain artist id which is the FK from artist table
        * session_id INT - This contain session id
        * location TEXT - This contain user location
        * user_agent TEXT - This contain browser that user used to access our service
    
        
## How to run the script


#### Instruction on how to perform the operation
1. every time before we peform etl.py we need to run create_tables.py first
2. then run etl.py using terminal command line "python etl.py"
3. check our inserted data and perfrom quries on database using test.ipynb

** do not forget to reset the kernel every time after finieshed running "test.ipynb"
        
        
## File in repository

#### Project data sources.
log_data and song_data directories is in the data directory. Inside log_data directory, it contains json file regarding application activity logs. Inside song_data directory, it contains json file regarding song information and artist information.


#### There are four files that we used to implement this project.
1. create_table.py # this file is run using terminal with follwing command line "python create_table.py". this file will first drop tables and create tables from sql_queries.py 
2. etl.py # this file will perform ETL operation to extract transform and load data into the database
3. sql_queries.py # this contains variables that contain Sequel query language (SQL) instructions to perform DROP, or CREATE TABLE and INSERT DATA INTO TABLES
4. test.ipynb # this note book can be used to test the connection of Sparkify database, and testing queries data to check whther we can find the data that we insert into the database.
