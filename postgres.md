### pg_dump
Dumping integrator db
```bash
pg_dump -h db-medisas -d integrator_production -U integrator_app -w -f prod_dump.sql
```

`pg_dump` a specific table
```bash
pg_dump -O -f out_file.sql -t <tablename> <dbname>
```

### psql
Basic connection (example from integrator app box uses .pgpass)
```bash
psql -w -h db-medisas -d integrator_production -U integrator_app
```

Restoring dump (from inside psql)
```plpgsql
\c <dbname>
\i integrator_prod_dump.sql
```
**OR**
edit owner of sql file and:
```bash
psql -d <dbname> -f file.sql
```

List databases
```plpgsql
\l
```

List tables
```plpgsql
\c <dbname>
\d+
```

Inspect table schema
```plpgsql
\d+ <tablename>
```

Basic insert
```plpgsql
INSERT INTO schema_migrations (version) VALUES ('123456');
```

Basic delete
```plpgsql
DELETE FROM schema_migrations WHERE version = '123456';
```

Check active connections
```plpgsql
SELECT * FROM pg_stat_activity;
```

Cancel query (after checking active connections)
```plpgsql
SELECT pg_cancel_backend(<pid of the postgres process>)
```

### Ubuntu packages

`postgresql-contrib` is required
```bash
sudo apt-get install postgresql-contrib
```

Check available extensions
```plpgsql
SELECT * FROM pg_available_extensions;
```

Install uuid extension if not installed (9.3 9.4)
```plpgsql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```