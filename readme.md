# Docker PostgreSQL DB instace

Compose and run a local docker postgreSQL DB instance where you can create new databases
in order to develop on local.

This project also has dump and restore instructions to easily create a insert data into a DB instance on docker on **dump_restore_postgres** folder.

## Docker Compose Setting 📋

_Get into postgres folder_

```
cd postgres
```

_There is a docker-compose file inside postgres **postgres/docker-compose.yml**_
_Inside this file you can see all the configurations to run a docker postgres instance_

### Importants Settings 

#### Docker Container Name 

```
container_name: postgres-docker-instance
```

#### Docker Enviroment parameters

```
environment:
- POSTGRES_DB=postgres
- POSTGRES_USER=postgres
- POSTGRES_PASSWORD={any_password}
```

#### Docker postgres ports

_If you have a local instance of postgres running on local probably your port 5432 is used, in that case you can put another port as inside port meanwhile the extern port must be always 5432_

inside:extern

```
ports:
    - "5433:5432"
```


## Run Docker Postgres Instance 🚀

	Open a new terminal on **postgres** folder a run docker 
	
	```
	docker-compose up
	```

	After this you can connect the DB using a DB Manager like dbeaver

	```
	https://dbeaver.io
	```

## Run Postgres commands on Docker

	In order to use postgres command like psql you have the following format:

	### Create DB

	```
  	docker exec <container_name> psql -U <postgres_user> -c "CREATE DATABASE <db_name>;"
  	```

  	### View Databases 

  	```
  	docker exec <container_name> psql -U <postgres_user> -l
  	```

