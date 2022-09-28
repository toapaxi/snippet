# Ejecutar instrucciones PSQL

psql -U postgres -f "C:\MENSEST\crear_usuario_system.sql"

### CREAR UNA TABLA A PARTIR DE UNA VISTA
CREATE TABLE view_aeronaves --TABLA A CREAR
AS TABLE view_aeronaves; --TABLA O VISTA A COPIAR


### AGREGAR PERMISOS A UN USUARIO
GRANT SELECT ON ALL TABLES IN SCHEMA public TO user;
