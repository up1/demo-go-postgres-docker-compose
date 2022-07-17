## Step to run

### Structure of project
* app 
  * Golang + Echo + connect to PostgreSQL
  * Use [Docker compose Wait](https://github.com/ufoscout/docker-compose-wait)
* migrate
  * Golang + Bun + connect to PostgreSQL
  * Use [Docker compose Wait](https://github.com/ufoscout/docker-compose-wait)
* db
  * PostgreSQL 10.14

### 1. Build Image
```
$docker compose build app
$docker compose build migrate
```

### 2. Create and run all containers
```
$docker compose up -d
$docker compose ps

NAME                              COMMAND                  SERVICE             STATUS              PORTS
question_go-community-app-1       "sh -c '/wait && ./b…"   app                 running             0.0.0.0:8000->80/tcp
question_go-community-db-1        "docker-entrypoint.s…"   db                  running             5432/tcp
question_go-community-migrate-1   "sh -c '/wait && ./m…"   migrate             exited (0)
```

Log of migrate
```
$docker compose logs migrate

question_go-community-migrate-1  | [INFO  wait] --------------------------------------------------------
question_go-community-migrate-1  | [INFO  wait]  docker-compose-wait 2.9.0
question_go-community-migrate-1  | [INFO  wait] ---------------------------
question_go-community-migrate-1  | [DEBUG wait] Starting with configuration:
question_go-community-migrate-1  | [DEBUG wait]  - Hosts to be waiting for: [db:5432]
question_go-community-migrate-1  | [DEBUG wait]  - Paths to be waiting for: []
question_go-community-migrate-1  | [DEBUG wait]  - Timeout before failure: 30 seconds 
question_go-community-migrate-1  | [DEBUG wait]  - TCP connection timeout before retry: 5 seconds 
question_go-community-migrate-1  | [DEBUG wait]  - Sleeping time before checking for hosts/paths availability: 0 seconds
question_go-community-migrate-1  | [DEBUG wait]  - Sleeping time once all hosts/paths are available: 0 seconds
question_go-community-migrate-1  | [DEBUG wait]  - Sleeping time between retries: 1 seconds
question_go-community-migrate-1  | [DEBUG wait] --------------------------------------------------------
question_go-community-migrate-1  | [INFO  wait] Checking availability of host [db:5432]
question_go-community-migrate-1  | [INFO  wait] Host [db:5432] not yet available...
question_go-community-migrate-1  | [INFO  wait] Host [db:5432] is now available!
question_go-community-migrate-1  | [INFO  wait] --------------------------------------------------------
question_go-community-migrate-1  | [INFO  wait] docker-compose-wait - Everything's fine, the application can now start!
question_go-community-migrate-1  | [INFO  wait] --------------------------------------------------------
question_go-community-migrate-1  | [bun]  16:58:49.953   SELECT               11.783ms  SELECT random()
question_go-community-migrate-1  | 0.699193783570081
question_go-community-migrate-1  | [INFO  wait] --------------------------------------------------------
question_go-community-migrate-1  | [INFO  wait]  docker-compose-wait 2.9.0
question_go-community-migrate-1  | [INFO  wait] ---------------------------
question_go-community-migrate-1  | [DEBUG wait] Starting with configuration:
question_go-community-migrate-1  | [DEBUG wait]  - Hosts to be waiting for: [db:5432]
question_go-community-migrate-1  | [DEBUG wait]  - Paths to be waiting for: []
question_go-community-migrate-1  | [DEBUG wait]  - Timeout before failure: 30 seconds 
question_go-community-migrate-1  | [DEBUG wait]  - TCP connection timeout before retry: 5 seconds 
question_go-community-migrate-1  | [DEBUG wait]  - Sleeping time before checking for hosts/paths availability: 0 seconds
question_go-community-migrate-1  | [DEBUG wait]  - Sleeping time once all hosts/paths are available: 0 seconds
question_go-community-migrate-1  | [DEBUG wait]  - Sleeping time between retries: 1 seconds
question_go-community-migrate-1  | [DEBUG wait] --------------------------------------------------------
question_go-community-migrate-1  | [INFO  wait] Checking availability of host [db:5432]
question_go-community-migrate-1  | [INFO  wait] Host [db:5432] not yet available...
question_go-community-migrate-1  | [INFO  wait] Host [db:5432] is now available!
question_go-community-migrate-1  | [INFO  wait] --------------------------------------------------------
question_go-community-migrate-1  | [INFO  wait] docker-compose-wait - Everything's fine, the application can now start!
question_go-community-migrate-1  | [INFO  wait] --------------------------------------------------------
question_go-community-migrate-1  | [bun]  17:04:00.212   SELECT                11.57ms  SELECT random()
question_go-community-migrate-1  | 0.976720210164785
```

