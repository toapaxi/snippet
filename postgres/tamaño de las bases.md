## Script para obtener el tamaño de la base de datos
SELECT datname AS nombre_db, pg_size_pretty(pg_database_size(datname)) AS tamaño
FROM pg_database
ORDER BY pg_database_size(datname) DESC;
