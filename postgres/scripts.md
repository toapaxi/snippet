# VER LAS TABLAS MAS GRANDES

```sql
SELECT
    table_schema || '.' || table_name AS table_full_name,
    pg_size_pretty(pg_total_relation_size(table_schema || '.' || table_name)) AS total_size,
    pg_size_pretty(pg_relation_size(table_schema || '.' || table_name)) AS table_size,
    pg_size_pretty(pg_total_relation_size(table_schema || '.' || table_name) - pg_relation_size(table_schema || '.' || table_name)) AS index_size
FROM
    information_schema.tables
WHERE
    table_schema NOT IN ('information_schema', 'pg_catalog')
ORDER BY
    pg_total_relation_size(table_schema || '.' || table_name) DESC
LIMIT 10;
```

# ELIMINAR SESIONES DE LA BASE
```sql
SELECT pg_terminate_backend(pid)
FROM pg_stat_activity
WHERE datname = 'odoo-ares'
AND pid <> pg_backend_pid();  -- evita que cierre tu propia sesión
```

# TAMAÑO DE LA BASE
```sql
SELECT pg_size_pretty(pg_database_size('odoo-ares')) AS size;
```

# BACKUP DE LA BASE
```sql
pg_dump -U postgres -d odoo-ares -F c -f odoo-ares.backup
```
# RESTORE DE LA BASE
```sql
pg_restore -U postgres -d odoo-relajo -1 odoo-ares.backup
```

