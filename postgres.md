# Ejecutar instrucciones PSQL

psql -U postgres -f "C:\MENSEST\crear_usuario_system.sql"

### CREAR UNA TABLA A PARTIR DE UNA VISTA
CREATE TABLE view_aeronaves --TABLA A CREAR
AS TABLE view_aeronaves; --TABLA O VISTA A COPIAR


### AGREGAR PERMISOS A UN USUARIO
GRANT SELECT ON ALL TABLES IN SCHEMA public TO user;


### CREATE COLLATION

CREATE COLLATION [ IF NOT EXISTS ] name (
    [ LOCALE = locale, ]
    [ LC_COLLATE = lc_collate, ]
    [ LC_CTYPE = lc_ctype, ]
    [ PROVIDER = provider, ]
    [ DETERMINISTIC = boolean, ]
    [ VERSION = version ]
)
CREATE COLLATION [ IF NOT EXISTS ] name FROM existing_collation

### PSQL: Realizar RESTORE de una BD usando archivo.sql

```
psql -U odoo -d sprint_08 -f dump.sql 
```