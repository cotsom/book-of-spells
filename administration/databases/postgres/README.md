# Postgres

## Secure PostgreSQL: Database, Patroni, Etcd and Pgbackrest

{% embed url="https://dincosman.com/2024/04/29/secure-postgresql-patroni/" %}

### Get not empty tables

```sql
DO $$
DECLARE
    r RECORD;
    row_count INT;
BEGIN
    FOR r IN SELECT tablename FROM pg_tables WHERE schemaname = 'public' LOOP
        EXECUTE format('SELECT COUNT(*) FROM %I', r.tablename) INTO row_count;
        IF row_count > 0 THEN
            RAISE NOTICE '%', r.tablename;
        END IF;
    END LOOP;
END $$;

```
