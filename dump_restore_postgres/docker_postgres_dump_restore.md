# DUMP FROM RDS DB POSTGRES AND RESTORE INTO A DOCKER POSTGRES DB

## DUMP

```
pg_dump -h <rds host> -p 5432 -F c -O -U <rds user> <db name> > db.dump
```

## DROP | CREATE DB

  In order to get a clean restore from dump file, I prefer to DROP and CREATE the database to restore.
  
  ```
  docker exec <container_name> psql -U <db_user> -c "DROP DATABASE <db_name>;"
  ```

  ```
  docker exec <container_name> psql -U <db_user> -c "CREATE DATABASE <db_name>;"
  ```

## PG_RESTORE (DUMP OR SQL FILES)

### COPY DUMP FILE INTO DOCKER POSTGRES VOLUME

#### Find Volume Path

  Localize 'Destination' key and get the volumen path from its key value

  ```
  docker inspect -f '{{ json .Mounts }}' <container_id> | python -m json.tool
  ```

#### Copy Dump File into Volume

  ```
  cp </path/to/dump/in/local> <container_name>:<path_to_volume>
  ```

### RESTORE DUMP INTO DOCKER DB

  ```
  docker exec <container_name> pg_restore -U <db_user> -d <db_name> <path_to_dump_on_docker>
  ```

## PSQL (SQL FILES) 

  ```
  cat dump.sql | docker exec -i <docker_id> psql -U <db_user> -d <db_name>
  ```

