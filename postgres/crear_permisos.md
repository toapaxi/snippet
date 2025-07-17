# CREACION DE PERMISOS 

## ROLES

CREATE ROLE grupo_lectura;
GRANT CONNECT ON DATABASE odoo-ares TO grupo_lectura;
GRANT USAGE ON SCHEMA public TO grupo_lectura;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO grupo_lectura;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO grupo_lectura;

### Asegurar que los permisos de lectura y escritura se otorguen por defecto a futuras tablas y secuencias creadas en el esquema `public`
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE ON TABLES TO grupo_lectura;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT USAGE, SELECT, UPDATE ON SEQUENCES TO grupo_lectura;

### Brindar permisos a una tabla
GRANT SELECT, INSERT, UPDATE, DELETE ON TABLE public.hr_trasbordo TO grupo_lectura;

## Crear el nuevo usuario
CREATE USER nuevo_usuario WITH PASSWORD '123.Y&rC8@vM9#s';

### Asignar el rol `grupo_lectura` al nuevo usuario
GRANT grupo_lectura TO nuevo_usuario;
