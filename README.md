A sample of PostgreSQL environment made by docker-compose

# Abstract
Sample PostgreSQL environment for [N-Yobikoh](https://www.nnn.ed.nico/pages/programming/)(Programming cource for novice)

# Set up
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

# Environment Variables 

## `docker-compose.yml`
|  Parameter  | Description | Default |
| ---  | --- | --- |
| `services.db.image` |  | `postgres:10-alpine` | 
| `services.db.container_name` |  | `postgres-container` | 

## `.env`
|  Parameter  | Description | Default |
| ---  | --- | --- |
| `POSTGRES_USER` |  | `postgres` | 
| `POSTGRES_PASSWORD` |  | `postgres` | 
| `POSTGRES_DB` |  | `testdb` | 
| `DATABASE_HOST` |  | `localhost` | 

# Reference
- http://docs.docker.jp/compose/compose-file.html#volume-configuration-reference
- https://matsuand.github.io/docs.docker.jp.onthefly/compose/compose-file/
