# Cambiar Parametros de configuracion en caliente

## Abrir PGADMIN y ejecutar
### En las siguientes sesiones se reflejaran los cambios
```sql
SHOW idle_session_timeout;

ALTER SYSTEM SET idle_session_timeout = '0';
SELECT pg_reload_conf();

SHOW idle_session_timeout;
```

```sql
SHOW idle_in_transaction_session_timeout;

ALTER SYSTEM SET idle_in_transaction_session_timeout = '0';
SELECT pg_reload_conf();

SHOW idle_in_transaction_session_timeout;
```
