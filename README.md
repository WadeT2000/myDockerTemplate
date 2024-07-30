# This is my Docker-Compose template

- Under docker-compose.yaml change my_database to the name of the database you want to create
    Line 9 - POSTGRES_DB=my_database
    Line 27 - DB_CONNECTION_STRING=postgresql://postgres:docker@db:5432/my_database 
      
- In ./api/.env change my_database to the name of the database you want to create as well.
      - DB_CONNECTION_STRING=postgresql://postgres:docker@db:5432/my_database

- All other ports and DockerFiles should be configured for 3000:3000 for the ui(frontend) and 8080:8080 for the api(backend). The database will be hosted on the defaul 5432:5432

- Knex, Cors and other dependecies are already written into the api folder.
    - If you want to run commands in the teminal you will have to run npm install within /api and /ui folder.


-Please read each ReadMe under each endpoint for additional information.