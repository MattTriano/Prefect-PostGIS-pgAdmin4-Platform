# Prefect-Postgres Platform

## Configuration

Create a blank `.env` file in this dir that defines the following environmental variables. (For the database connection var, you'll probably want to swap in the actual value, even though it's kind of redundant).

```bash
POSTGRES_USER=<your_desired_db_user_name>
POSTGRES_PASSWORD=<a_password_for_the_database>
POSTGRES_DB=<your_desired_database_name>
PGADMIN_DEFAULT_EMAIL=<an_email>
PGADMIN_DEFAULT_PASSWORD=<a_password_for_the_db_admin_interface>
PREFECT_ORION_API_HOST=0.0.0.0
PREFECT_ORION_DATABASE_CONNECTION_URL=postgresql+asyncpg://${POSTGRES_USER}:${POSTGRES_PASSWORD}@<name_of_the_db_service_from_docker-compose.yml>:5432/${POSTGRES_DB}
```

After setting credentials for the database build the application and then start it up

```bash
$ docker-compose up --build
```

If you run into issues in the initial setup, you'll probably to just start fresh, which can easily be achieved by the following command (note: the `-v` flag purges volumes defined in the `docker-compose.yml` file).

```bash
$ docker-compose down -v
```

Then you'll be able to connect to the database via port 5432 (or whatever port you set as the database-host port in the `docker-compose.yml` file) and access the admin portal at http://0.0.0.0:5678 (or whatever port you set as the admin-host port in the `docker-compose.yml` file).


## Accessing the Prefect CLI

Via a terminal in the working dir containing this README, use the command below to run the `prefect_cli` service

```bash
$ docker-compose run prefect_cli
```

This should give you a bash shell in the `~/flows` directory in the prefect container, and you can run flows via 

```bash
user@host:~/flows# python <flow_name>.py
```

## Accessing the Prefect Web UI

If the server is running and the setup ran without throwing errors, you can access the Prefect UI at [http://0.0.0.0:4200/](http://0.0.0.0:4200/) (if you used a different port number, swap that in place of the 4200).

## Accessing the pgAdmin4 Admin UI

Access the interface at [http://0.0.0.0:5678/](http://0.0.0.0:5678/) and enter the credentials defined in the `.env` file that start with PGADMIN_...


# Referenced Material:

* [rpden's docker-compose prefect repo](https://github.com/rpeden/prefect-docker-compose)