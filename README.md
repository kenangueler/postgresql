# PostgreSQL for Local Development

PostgreSQL containers for local development.

Services
- PostgreSQL 17
- pgAdmin 4 latest

Prerequisites
- Docker (or Podman) installed and running
- Docker Compose (or `docker compose` support)
- Optional: `psql` client to connect from the host

Environment
- Copy `.env.example` to `.env` (will be auto-loaded by docker compose) or export as environment variables:
  - POSTGRES_USER
  - POSTGRES_PASSWORD
  - POSTGRES_DB
  - POSTGRES_EXPOSE_HOST
  - POSTGRES_EXPOSE_PORT

Quick startQuick start
1. Create a `.env` file with the variables above (or export them in your shell).
2. Start the containers:

```bash
docker compose up -d
```

3. Stop the containers:

```bash
docker compose down
```

Common commands
- View logs: `docker compose logs -f`
- Connect from host with `psql`:

```bash
psql "host=localhost user=$POSTGRES_USER dbname=$POSTGRES_DB"
```

- Reset data (removes volumes): `docker compose down -v`
- Change ports, volumes, or credentials in `docker-compose.yml` as needed.

Database connection
- PostgreSQL server image: 17
- Internal container port: `5432`
- Host port: the value of `POSTGRES_PORT` in your `.env` (default in this repo: `15432`)

### PostgreSQL connection (example)

- Host: `localhost` (or `127.0.0.1`)
- Port: `5432` (container). When connecting from the host use your `POSTGRES_PORT` (e.g. `15432`).
- Database: `test`
- User: `test`
- Password: `test`

### pgAdmin web interface

Access pgAdmin at: http://localhost:5050

- Email: `test@localhost`
- Password: `password`

To connect to PostgreSQL from pgAdmin:
1. Add a new server in pgAdmin.
2. In the **General** tab set **Name** to `testDB` (or any name).
3. In the **Connection** tab set:
   - **Host**: `postgres` (the compose service name, reachable from pgAdmin container)
   - **Port**: `5432` (internal container port)
   - **Maintenance database**: `postgres`
   - **Username**: `test`
   - **Password**: `test` (toggle "Save password" if you want)

You should then see `testDB` in the Servers view with the `test` and `postgres` databases.

