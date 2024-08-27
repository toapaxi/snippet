#  CREAR LA EXTENSION EN LA BASE

CREATE EXTENSION IF NOT EXISTS pg_stat_statements
    SCHEMA public
    VERSION "1.9";

# HABILITAR EN POSTGRES.CONF


shared_preload_libraries = 'pg_stat_statements'  # (change requires restart) 
pg_stat_statements.track = all


--Consultas Lentas
SELECT total_exec_time, mean_exec_time, calls, query
FROM pg_stat_statements
ORDER BY total_exec_time DESC
LIMIT 10;

--Consultas Frecuentes:

SELECT query, calls, total_exec_time, mean_exec_time
FROM pg_stat_statements
ORDER BY calls DESC
LIMIT 10;

--Consultas con Alto I/O:

SELECT query, shared_blks_read, shared_blks_hit, temp_blks_written
FROM pg_stat_statements
ORDER BY shared_blks_read DESC
LIMIT 10;
