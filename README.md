# dev-academy-spring-2024-exercise

This is the pre-assignment for Solita Dev Academy Finland January 2024. But if you’re here just purely out of curiosity, feel free to snatch the idea and make your own city bike app just for the fun of it!

Let's imagine that you have received an interesting project offer to create a UI and a backend service for displaying data from journeys made with city bikes in the Helsinki Capital area.

The exercise uses data that is owned by City Bike Finland. We provide database to you in a Docker container, but the original datasets can be downloaded from here:

- https://dev.hsl.fi/citybikes/od-trips-2021/2021-05.csv
- https://dev.hsl.fi/citybikes/od-trips-2021/2021-06.csv
- https://dev.hsl.fi/citybikes/od-trips-2021/2021-07.csv

Also, the database is created using dataset that has information about Helsinki Region Transport’s (HSL) city bicycle stations.

- Dataset: https://opendata.arcgis.com/datasets/726277c507ef4914b0aec3cbcfcbfafc_0.csv
- License and information: https://www.avoindata.fi/data/en/dataset/hsl-n-kaupunkipyoraasemat/resource/a23eef3a-cc40-4608-8aa2-c730d17e8902

# The exercise
Create a web application that uses a backend service to fetch the data. Backend can be made with any technology. We at Solita use for example (not in preference order) Java/Kotlin/C#/TypeScript but you are free to choose any other technology as well.

You are provided with Docker setup, with contains a PostgreSQL database with all the necessary data for the exercise. 

You can also freely choose the frontend technologies to use. The important part is to give good instructions on how to build and run the project.

Please return the exercise as a link to github repository. 

# Functional requirements
## Station list
- List all stations
- Link to single station views

## Single station view
- Station name
- Station address
- Total number of journeys starting from the station
- Total number of journeys ending at the station
- Average distance of journeys starting from the station
- Avarage duration of journeys starting from the station

# Instructions for running the database
1. Install Docker Desktop on your computer (https://docs.docker.com/desktop/)
2. Clone this repository
3. On command line under this folder run:

```
docker compose up --build --renew-anon-volumes -d
```

Please note that running that might take couple of minutes

4. Docker setup also comes with Adminer UI, where you can check your database contents at http://localhost:8088/
5. Log into Adminer with following information (password: academy):

![alt text](login.png)

Database is running at postgres://localhost:5432/citybike and the database name is citybike. Database comes with user academy (password: academy).

# Database structure
Database consists of two tables: station and journey.

## Station table
| Column | Description | Type |
| ----------- | ----------- | ----------- |
| id | id, primary key | integer |
| station_name | Name of the station | character varying(100) *NULL* |
| station_address | Address of the station | character varying(100) *NULL* |
| coordinate_x | X coordinate of the station | character varying(100) *NULL* |
| coordinate_y | Y coordinate of the station | character varying(100) *NULL* |

## Journey table
| Column | Description | Type |
| ----------- | ----------- | ----------- |
| id | id, primary key | integer |
| departure_date_time | Journey start timestamp | timestamp *NULL* |
| return_date_time | Journey end timestamp | timestamp *NULL* |
| departure_station_id | Journey start station | integer, references to station(id) |
| return_station_id | Journey end station | integer, references to station(id) |
| distance | Distance of journey in meters | integer *NULL* |
| duration | Duration of journey in seconds | integer *NULL* |
