# This is my Docker-Compose template

- Under docker-compose.yaml change my_database to the name of the database you want to create
    Line 10 - POSTGRES_DB=my_database
    Line 35 - DB_CONNECTION_STRING=postgresql://postgres:docker@db:5432/my_database 
    (Save the document)
      
- In ./api/.env change my_database to the name of the database you want to create as well.
      - DB_CONNECTION_STRING=postgresql://postgres:docker@db:5432/my_database

- All other ports and DockerFiles should be configured for 3000:3000 for the ui(frontend) and 8080:8080 for the api(backend). The database will be hosted on the default 5432:5432

# First step before running
    
    Open docker-desktop in the background
        
        (Windows Users)
        -Navigate to settings
            - Navigate to resources, then WSL integration
            - Ensure the Enable checkbox is selected and your terminal is selected as well.


    In the VS Code terminal:
        - CD into the api folder and run 'npm install'
        - CD into the ui folder and run 'npm install'

    After running npm install for each endpoint, in the terminal CD back to mydockertemplate and do the following:

        1. ` docker-compose up --build `

Before we start creating our front and backend lets check to make sure our database hase been build properly.

If you have an error in your terminal see below.

# Common Errors

1. If you run into the issue of already having a container with this name follow directions below
            The container name "/db" is already in use by container "---------------------------------------". You have to remove (or rename) that container to be able to reuse that name.

            - Navigate to docker-compose.yaml and change the container name on Line 4

            OR

            - In the terminal 
                - Press Lctrl+C
                + ` docker container rm <Container Name> ` (Container Name should be the container that is being hosted on the same port)
                (This should resolve your container issues)

 2. Database that you've created not actually being created? follow below instructions
    (db   | 2024-08-05 18:43:43.441 UTC [40] FATAL:  database "<Your database name>" does not exist)
    There are two main ways to go about this fix actions
        1. Manually create your database:
        - Now that you have created a db container lets look inside it.
            - Open a new terminal
                + ` docker ps `
                (you should see a couple containers listed, one of them should have the name db with a container id similar to <6d3nna456...> this will change with every container you spin up)
                + ` docker exec -it <First 2-4 digits in the container ID> bash `
                + ` psql -U postgres `
                + ` \l `
                (This should produce a chart of all the database under your current container)
                + ` CREATE DATABASE <Database name that you have come up with in the previous steps matching this name is important> ; `
            You have now created your database.
                - In your main terminal
                    + Press L-ctrl + C 
                    + ` docker-compose down `
                    + ` docker-compose up --build `
            Everything should be up and running as intended.

        2. Delete all previous volumes so it creates your database upon starting your application
            (Be warned this will delete any previous databases that you have build in your user-data directory, if you dont have anything personal that you have build and want to keep then avoid doing this step)
            
            - In your current terminal
                + Press L-ctrl + C
                + ` docker-compose down -v `
                + ` docker-compose up --build `
            Everything should be up and running as intended




                    

# The application should be up and running

    Your basic testing application should be running
        localhost:3000/ should display 
            - Testing
        localhost:8080/ should display
                - My API is up and running!
            As well as and end point
        localhost:8080/testingtable
                - [{"id":1,"name":"rowValue1"},{"id":2,"name":"rowValue2"},{"id":3,"name":"rowValue3"}]


    To close down the application in VS Code terminal
        1. ` docker-compose down `



-Please read each ReadMe under each endpoint for additional information on making changes to the front/back end of your application.



# Navigating docker-compose

    From here you can build your Frontend(ui) and backend(api)
    Follow the Readme's for each directory to build your database and react-app

Once you have completed your database run ` docker-compose up --build `
You can work on your app.js to make you endpoints and everything under ui/src to make your front and and it will show your changes at each localhost:<port>.

    (Keep in mind and changes to the actual database you will need to ` docker-compose down ` and ` docker-compose up --build ` to see these new changes)