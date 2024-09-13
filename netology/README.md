# Description
Here are simple guides on how to create useful things with Docker and manage them efficiently.

## how to create db aviaperevozki ?

download db from https://postgrespro.ru/docs/postgrespro/10/demodb-bookings-installation

*1.Enter to docker*

docker exec -it <container id> bash

*2. Run sql script*

psql -f /tmp/backup.sql -U <username> -d demo


## how to enter into postgres db which is in docker container?
*Step 1: List running Docker containers*

docker ps

*Step 2: Access the PostgreSQL container (replace <container_id_or_name> with actual ID or name)*

docker exec -it <container_id_or_name> bash

*Step 3: Connect to PostgreSQL (replace <username> and <database_name> with actual values)*

psql -U <username> -d <database_name>


## how to create new server postgres inside existing container?
*Step 1: Access the PostgreSQL container*

docker exec -it abc123 bash

*Step 2: Connect to PostgreSQL*
psql -U user -d database

*Step 3: Create a new database*
CREATE DATABASE new_database_name;

## how to upload database dump via psql if postgres is inside docker container?
*Step 1: Copy the dump file into the container*

docker cp backup.sql abc123:/tmp/backup.sql

*Step 2: Access the PostgreSQL container*

docker exec -it abc123 bash

*Step 3: Upload the dump*

psql -U postgres -d mydatabase -f /tmp/backup.sql

## how to make up a back up of my data into the docker container with postgres db?

*Step 1: Access the PostgreSQL container*

docker exec -it 23922b6dcba0 bash

*Step 2: Run pg_dump to create a backup*

pg_dump -U username -d database_name -F c -f /tmp/backup.dump

*Step 3: Exit the container*

exit

*Step 4: Copy the backup file to the host machine*

docker cp my_training_psql:/tmp/backup.dump ./backup.dump

**Explanation**
- __docker exec -it my_training_psql bash:__ Opens a bash shell in the container named my_training_psql.
- __pg_dump -U postgres -d mydatabase -F c -f /tmp/backup.dump:__ Creates a backup of the mydatabase database using the postgres user. The -F c option specifies the custom format for the backup, and -f /tmp/backup.dump specifies the output file.
- __docker cp my_training_psql:/tmp/backup.dump ./backup.dump:__ Copies the backup file from the container to the current directory on the host machine.