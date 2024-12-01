# Docker PostgreSQL Setup

This is a simple Docker Compose configuration for running PostgreSQL with persistent data storage.

## Configuration Details

- PostgreSQL Version: Latest
- Default Port: 5432
- Default Database: mydb
- Default User: postgres
- Default Password: postgres

## Environment Variables

The configuration uses environment variables defined in `.env` file. To get started:

1. Copy `.env.example` to `.env`:

   Linux/macOS:
   ```bash
   cp .env.example .env
   ```

   Windows (Command Prompt):
   ```cmd
   copy .env.example .env
   ```

   Windows (PowerShell):
   ```powershell
   Copy-Item .env.example .env
   ```

2. Modify the values in `.env` according to your needs:
   - `POSTGRES_VERSION`: PostgreSQL version (default: 14)
   - `POSTGRES_USER`: Database user (default: postgres)
   - `POSTGRES_PASSWORD`: Database password (default: postgres)
   - `POSTGRES_DB`: Default database name (default: mydb)
   - `POSTGRES_PORT`: Internal PostgreSQL port (default: 5432)
   - `HOST_PORT`: Host machine port mapping (default: 5433)

Note: The `.env` file is ignored by git for security reasons. Never commit sensitive credentials to version control.

## Volume Information

The configuration uses a named volume `postgres_data` to persist the database data. This ensures your data remains intact even if the container is removed.

## How to Use

1. Start the PostgreSQL container:
   ```bash
   docker-compose up -d
   ```

2. Stop the container:
   ```bash
   docker-compose down
   ```

3. To completely remove the container and volume:
   ```bash
   docker-compose down -v
   ```

## Connecting to the Database

### Local Connection
- Host: localhost
- Port: 5433 (configurable via HOST_PORT in .env)
- Database: mydb (configurable via POSTGRES_DB in .env)
- Username: postgres (configurable via POSTGRES_USER in .env)
- Password: postgres (configurable via POSTGRES_PASSWORD in .env)

### Remote Connection
To connect from another server, use the host machine's IP address or domain name instead of localhost:
- Host: <your-server-ip-address>
- Port: 5433 (configurable via HOST_PORT in .env)
- Database: mydb (configurable via POSTGRES_DB in .env)
- Username: postgres (configurable via POSTGRES_USER in .env)
- Password: postgres (configurable via POSTGRES_PASSWORD in .env)

Example connection string:
```
postgresql://postgres:postgres@your-server-ip:5433/mydb
```

### Security Considerations
1. Make sure your firewall allows incoming connections on the PostgreSQL port (default: 5433)
2. Use strong passwords in production
3. Consider using SSL for secure connections
4. Restrict IP addresses in pg_hba.conf for production environments

You can connect to the database using any PostgreSQL client like pgAdmin, DBeaver, or the psql command line tool.
