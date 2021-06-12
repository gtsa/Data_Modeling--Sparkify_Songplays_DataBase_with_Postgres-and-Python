## Sparkify Data Modeling with Postgres

Wanting to analyze the data we've been collecting on songs and user activity on our new music streaming app, Sparkify's analytics team is particularly interested in understanding what songs users are listening to. 

Since until recently we didn't have an easy way to query our data - which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app - we created a Postgres database with tables designed to optimize queries on song play analysis

To do so, and given that:

- the simple relationships between our data,
- the relatively small size of our database (**sparkifydb**), and
- our analytical focus favors and is favored by simpler and faster SQL queries on song play analysis

we chose to arrange our data in a star schema structure in Postgres, building as well an ETL pipeline that transfers data from files in two local directories into the tables/relations of our schema using Python and SQL.

So, our schema consists of the following tables:

- **Fact Table**
    
    1. songplays - records in log data associated with song plays i.e. records with page "NextSong"
        - *songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent*

- **Dimension Tables**
    
    2. users - users in the app
        - *user_id, first_name, last_name, gender, level*
    
    3. songs - songs in music database
        - *song_id, title, artist_id, year, duration*
    
    4. artists - artists in music database
        - *artist_id, name, location, latitude, longitude*
    
    5. time - timestamps of records in songplays broken down into specific units
        - *start_time, hour, day, week, month, year, weekday*
        
--------------------

#### Files in the respository

Our repository consists of the following files:
1. **Data** files (***data*** folder)
    - ***log_data*** folder
    - ***song_data*** folder
2. **Python** files (***.py***)
    - ***sql_queries.py*** (contains all our sql queries that are imported into the following two files,
    - ***create_tables.py*** (drops and creates our tables. We run this file to reset our tables before each time we run our ETL scripts,
    - ***etl.py*** (reads and processes files from song_data and log_data and loads them into our tables
3. **Jupyter Notebook** files (***.ipynb***)
    - ***test.ipynb*** (dedicated - either with its SQL queries, or as a draft notebook to write others - to let anyone check our database)
    - ***etl.ipynb*** (consice presentation/outline of the steps and methodology of our ETL pipeline building

---------------------

#### Instructions on how to run the scripts
For someone to build an image of our database (*sparkifydb*) and its star-structured schema of 5 tables (1 fact and 4 dimension ones), they must follow **serially** the following three steps:
   
   1. Lauch a command-line interface (terminal)
   
   2. Run ***create_tables.py*** (command: *python create_tables.py*)
   
   3. Run ***etl.py*** (command: *python create_tables.py*)
   
    **\*** The database can be explored and tested via ***test.ipynb***

#### Query Examples

- *SELECT \* FROM songplays LIMIT 5;*

- *SELECT \* FROM users LIMIT 5;*

- *SELECT \* FROM songs LIMIT 5;*

- *SELECT \* FROM artists LIMIT 5;*

- *SELECT \* FROM time LIMIT 5;*

