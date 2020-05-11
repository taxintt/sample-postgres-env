A sample of PostgreSQL environment made by docker-compose

## Abstract
Sample PostgreSQL environment for [N-Yobikoh](https://www.nnn.ed.nico/pages/programming/)(Programming cource for novice).<br>
You don't need to create user and run command for making database(`secret_board`).

## Set up
You need to [install docker](https://docs.docker.com/get-docker/) in advance.

Step 1: Clone the repo

```
$ git clone https://github.com/TaxiN/sample-postgres-env

$ cd ./postgre_env
```


Step 2: Create and run the postgres container (`docker-compose up`)
```
$ docker-compose up -d
```

Step 3: Run command to start bash session in the container 

```
$ docker container ls -a
CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS                   PORTS                       NAMES
88d645d50d44        postgres:10-alpine     "docker-entrypoint.s…"   26 seconds ago      Up 25 seconds            0.0.0.0:5432->5432/tcp      postgres-container

$ docker exec -it 88d645d50d44 /bin/bash
```

Step 4: Switch to `postgres` user and check database 

```
bash-5.0# su - postgres
88d645d50d44:~$ 
88d645d50d44:~$ psql
psql (10.12)
Type "help" for help.

// already made database(secret_board)
postgres=# \l
                                  List of databases
     Name     |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
--------------+----------+----------+------------+------------+-----------------------
 postgres     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 secret_board | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0    | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
              |          |          |            |            | postgres=CTc/postgres
 template1    | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
              |          |          |            |            | postgres=CTc/postgres
 testdb       | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
(5 rows)
```

In [sample application (Node.js)](https://github.com/progedu/secret-board-3022), just specified connection URL.

```
const sequelize = new Sequelize(
    'postgres://postgres:postgres@localhost:5432/secret_board', 
    {
        logging: false
    }
);
```

To delete the intance, run the following command.

```
$ docker-compose down -v
```

## Environment Variables 

`docker-compose.yml`
|  Parameter  | Description | Default |
| ---  | --- | --- |
| `services.db.image` | the version of Postgres image  | `postgres:10-alpine` | 
| `services.db.container_name` | name of the Postgres container | `postgres-container` | 

`.env`
|  Parameter  | Description | Default |
| ---  | --- | --- |
| `POSTGRES_USER` | the superuser's name for PostgreSQL.  | `postgres` | 
| `POSTGRES_PASSWORD` | the superuser password for PostgreSQL | `postgres` | 
| `POSTGRES_DB` | the default database that is created when the image is first started | `testdb` | 
| `DATABASE_HOST` | the hostname of database instance | `test_instance` | 

## Reference
- http://docs.docker.jp/compose/compose-file.html#volume-configuration-reference
- https://matsuand.github.io/docs.docker.jp.onthefly/compose/compose-file/
- https://hub.docker.com/_/postgres
