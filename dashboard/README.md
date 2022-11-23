# Dashboard deployment

Basically the deployment of dashboard(frontend and backend) can be done by just entering the dirs, modify the essential environment variables and launch the docker services by docker-compose:

```bash
$ cd dashboard/frontend
$ docker-compose -f docker-compose.yml up -d

$ cd -

# edit the docker-compose.yml's environment vars before launching
$ cd dashboard/backend
$ docker-compose -f docker-compose.yml up -d
```



## Frontend Configs

The web front page is made up of some compiled js, css files, then hosted statically by nginx. Usually no additional modifications is need to make it run. While the only point to care, is that the default API calls (url with prefix `/api`) is redirected to backend `http://dashboard-backend-nodejs:8008`, which can be found in the sample nginx configs in `frontend` folder. So just keep the redirected host name and port binding the same with the that in backend compose files.



## Backend Configs

Since backend connects various services to feed data to front, there are several blocks of configs in the compose yaml file:

      # The airflow API server
      - AIRFLOW_API_URL="http://YOUR_AIRFLOW_SERVER:8080"
      - AIRFLOW_USER=YOUR_AIRFLOW_USER
      - AIRFLOW_PASSWORD=YOUR_AIRFLOW_PASSWORD
    
      # The clickhouse connection info
      - CK_HOST=YOUR_CLICKHOUSE_HOST
      - CK_PORT=YOUR_CLICKHOUSE_PORT
      - CK_USER=YOUR_CLICKHOUSE_USER
      - CK_PASS=YOUR_CLICKHOUSE_PASSOWRD
    
      # The postgresql connection info
      - PGHOST=YOUR_POSTGRES_DB_HOST
      - PGPORT=5432
      - PGDATABASE=YOUR_POSTGRES_DB_NAME
      - PGPASSWORD=YOUR_POSTGRES_DB_PWD
      - PGUSER=YOUR_POSTGRES_DB_USER