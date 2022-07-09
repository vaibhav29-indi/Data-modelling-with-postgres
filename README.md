Project Information - 

- Introduction

•A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

•They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and    bring you on the project. Your role is to create a database schema and ETL pipeline for this analysis. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.
Project Description

•In this project, you'll apply what you've learned on data modeling with Postgres and build an ETL pipeline using Python. To complete the project, you will need to define fact and dimension tables for a star schema for a particular analytic focus, and write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL. 


- Data Mapping-

  - Fact Table

    - songplays - records in log data associated with song plays i.e. records with page NextSong
        songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

  - Dimension Tables

    - users - users in the app
        user_id, first_name, last_name, gender, level
    - songs - songs in music database
        song_id, title, artist_id, year, duration
    - artists - artists in music database
        artist_id, name, location, latitude, longitude
    - time - timestamps of records in songplays broken down into specific units
        start_time, hour, day, week, month, year, weekday


In addition to the data files, the project workspace includes six files:

1.  test.ipynb is used for testing and doing sanity check for all the data tha gets inserted to db via the ETL pipeline
2.  create_tables.py drops and creates the tables. This is alo used for resetting the connection to the tables in case of issues
3.  etl.ipynb is for developing the model and doing regression to see if all the data is successfully added to the db.Once the etl is setup and tested for singe rows, it is replicated into etl.py
4.  etl.py is responsible for setting up the ETL pipeline and transfers data from data/song and data/log folders to the database.
5.  sql_queries.py contains all the sql queries, and is imported into the last three files above.
6.  README.md provides broad outline and coverage for the project.


![This is diagram for the database mapping](https://drive.google.com/file/d/1IRAwhvVpjvglrUZy6N1Ren67r_9Uy5Iq/view?usp=sharing)

- Interconnection of Pipeline -

In this project, I was introduced to working with Data pipelines.
- Database flavour used for this project is Postgres which is a flavour of SQL databased.
- Python was used for setting up the ETL pipeline, ETL stands for Extract, Transform and Load.
- Relevance of ETL in this project can be explained as follows-
    - The Data was stored in the data/song and data/log folders respectively.
    - Data/song folder had json files which were consumed for populating the rows under the sonfs and artists dimension tables.
    - Data/log folder had files which were consumed for populating the rows under the time, users dimension tables and songplays fact table.
    - The extraction of data was done through the selection of columns from the pandas dataframe which in turn were created using read_json method of pandas
    - The transformation was done using the methods available in pandas library for say change of data type, limit the number of rows, extracting date,month,year,etc from the values in specific columns.
    - Ultimately the loading of relevant data to the database happened through the INSERT queries into the tables which were initially defined with CREATE queries.
    
Execution of the scripts :

- From the side menu in jupyter notebook workspace, click + sign.
- This opens the Launcher window, from here we cann choose the Terminal option.
- Terminal option should dispaly the prompt such as 
  - root@f54e77272a39:/home/workspace# 
  This means we are in workspace, all the python files are in the same directory and can be accessed from same directory.
- Type python create_tables.py for dropping(if tables exist), recreating all the fact and dimension tables for our usage.
- From the side menu double click on the test.ipynb and run first two queries, this will eb sanity test that database is connected and ready.
- In the same terminal that was used for executing the create_tables.py , Type python etl.py
  This should complete the extraction, transformation and loading of the data from data/song and data/log folders into the database.
- Finally continue running the test.ipynb file to validate that all the data was inserted into the database and meets our expectation.


References -

Throughout this challenging project the references were made to multiple sources such as - 
https://stackoverflow.com/questions/41783003/how-do-i-convert-timestamp-to-datetime-date-in-pandas-dataframe
https://pandas.pydata.org/docs/reference/api/pandas.to_datetime.html
https://www.geeksforgeeks.org/python-pandas-series-dt-year/
https://www.geeksforgeeks.org/python-pandas-series-dt-year/
https://www.geeksforgeeks.org/filter-pandas-dataframe-with-multiple-conditions/
https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-upsert/