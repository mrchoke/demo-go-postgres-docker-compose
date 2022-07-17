# Step to run

## Structure of project
* app 
  * Golang + Echo + connect to PostgreSQL
* migrate
  * Golang + Bun + connect to PostgreSQL
* db
  * PostgreSQL 10.14

## 1. Build Image
```
$docker compose build app
$docker compose build migrate
```

## 2. Create and run all containers
```
$docker compose up -d
$docker compose ps

NAME                                        COMMAND                  SERVICE             STATUS              PORTS
demo-go-postgres-docker-compose-app-1       "sh -c ./backend"        app                 running             0.0.0.0:8000->1323/tcp, :::8000->1323/tcp
demo-go-postgres-docker-compose-db-1        "docker-entrypoint.s…"   db                  running (healthy)   5432/tcp
demo-go-postgres-docker-compose-migrate-1   "sh -c ./migrate"        migrate             exited (0)
```

## 3. Test API

```
curl localhost:8000
Hello, World
```

## Logs

### Log of migrate
```
$docker compose logs migrate

demo-go-postgres-docker-compose-migrate-1  | 0.278793987352401
demo-go-postgres-docker-compose-migrate-1  | [bun]  18:15:07.943   SELECT                2.256ms  SELECT random()
```

### Log of app
```
$docker-compose logs app

demo-go-postgres-docker-compose-app-1  | Successfully connected!
demo-go-postgres-docker-compose-app-1  |
demo-go-postgres-docker-compose-app-1  |    ____    __
demo-go-postgres-docker-compose-app-1  |   / __/___/ /  ___
demo-go-postgres-docker-compose-app-1  |  / _// __/ _ \/ _ \
demo-go-postgres-docker-compose-app-1  | /___/\__/_//_/\___/ v4.7.2
demo-go-postgres-docker-compose-app-1  | High performance, minimalist Go web framework
demo-go-postgres-docker-compose-app-1  | https://echo.labstack.com
demo-go-postgres-docker-compose-app-1  | ____________________________________O/_______
demo-go-postgres-docker-compose-app-1  |                                     O\
demo-go-postgres-docker-compose-app-1  | ⇨ http server started on [::]:1323
```

### Log of db
```
docker-compose logs db

demo-go-postgres-docker-compose-db-1  | The files belonging to this database system will be owned by user "postgres".
demo-go-postgres-docker-compose-db-1  | This user must also own the server process.
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  | The database cluster will be initialized with locale "en_US.utf8".
demo-go-postgres-docker-compose-db-1  | The default database encoding has accordingly been set to "UTF8".
demo-go-postgres-docker-compose-db-1  | The default text search configuration will be set to "english".
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  | Data page checksums are disabled.
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  | fixing permissions on existing directory /var/lib/postgresql/data ... ok
demo-go-postgres-docker-compose-db-1  | creating subdirectories ... ok
demo-go-postgres-docker-compose-db-1  | selecting default max_connections ... 100
demo-go-postgres-docker-compose-db-1  | selecting default shared_buffers ... 128MB
demo-go-postgres-docker-compose-db-1  | selecting default timezone ... Etc/UTC
demo-go-postgres-docker-compose-db-1  | selecting dynamic shared memory implementation ... posix
demo-go-postgres-docker-compose-db-1  | creating configuration files ... ok
demo-go-postgres-docker-compose-db-1  | running bootstrap script ... ok
demo-go-postgres-docker-compose-db-1  | performing post-bootstrap initialization ... ok
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  | WARNING: enabling "trust" authentication for local connections
demo-go-postgres-docker-compose-db-1  | You can change this by editing pg_hba.conf or using the option -A, or
demo-go-postgres-docker-compose-db-1  | --auth-local and --auth-host, the next time you run initdb.
demo-go-postgres-docker-compose-db-1  | syncing data to disk ... ok
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  | Success. You can now start the database server using:
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  |     pg_ctl -D /var/lib/postgresql/data -l logfile start
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  | waiting for server to start....2022-07-17 18:15:02.084 UTC [61] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.210 UTC [62] LOG:  database system was shut down at 2022-07-17 18:14:37 UTC
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.238 UTC [61] LOG:  database system is ready to accept connections
demo-go-postgres-docker-compose-db-1  |  done
demo-go-postgres-docker-compose-db-1  | server started
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  | /usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/*
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  | waiting for server to shut down....2022-07-17 18:15:02.254 UTC [61] LOG:  received fast shutdown request
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.278 UTC [61] LOG:  aborting any active transactions
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.282 UTC [61] LOG:  worker process: logical replication launcher (PID 68) exited with exit code 1
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.282 UTC [63] LOG:  shutting down
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.496 UTC [61] LOG:  database system is shut down
demo-go-postgres-docker-compose-db-1  |  done
demo-go-postgres-docker-compose-db-1  | server stopped
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  | PostgreSQL init process complete; ready for start up.
demo-go-postgres-docker-compose-db-1  |
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.697 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.697 UTC [1] LOG:  listening on IPv6 address "::", port 5432
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.742 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.822 UTC [70] LOG:  database system was shut down at 2022-07-17 18:15:02 UTC
demo-go-postgres-docker-compose-db-1  | 2022-07-17 18:15:02.851 UTC [1] LOG:  database system is ready to accept connection
```
