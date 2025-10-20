## Script para obtener el tamaño de la base de datos


SELECT datname AS nombre_db, pg_size_pretty(pg_database_size(datname)) AS tamaño
FROM pg_database
ORDER BY pg_database_size(datname) DESC;

## Script para obtener el tamaño de las tablas
SELECT
    schemaname,
    relname,
    pg_size_pretty(pg_total_relation_size(relid)) AS tamano_total
FROM pg_catalog.pg_statio_user_tables
ORDER BY pg_total_relation_size(relid) DESC
LIMIT 20;
