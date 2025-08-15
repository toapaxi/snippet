# VER LOS PERMISOS DE CADA ROL
> reemplazar saquito por el nuevo rol
```psql

-- Tablas y vistas
SELECT 
    grantee AS rol,
    privilege_type AS permiso,
    table_schema AS esquema,
    table_name AS objeto,
    'TABLE/VIEW' AS tipo
FROM information_schema.role_table_grants
WHERE grantee = 'saquito'

UNION ALL

-- Funciones
SELECT 
    grantee,
    privilege_type,
    routine_schema AS esquema,
    routine_name AS objeto,
    'FUNCTION' AS tipo
FROM information_schema.role_routine_grants
WHERE grantee = 'saquito'

UNION ALL

-- Secuencias (usando ACLs del catálogo)
SELECT 
    grantee.rolname AS rol,
    privilege_type.privilege AS permiso,
    nspname AS esquema,
    relname AS objeto,
    'SEQUENCE' AS tipo
FROM pg_class c
JOIN pg_namespace n ON n.oid = c.relnamespace
JOIN pg_roles grantee ON true
CROSS JOIN LATERAL (
    SELECT unnest(string_to_array(replace(replace(replace(
        regexp_replace(acl::text, '^"|"$', '', 'g'),
        'saquito=', ''),
        'postgres=', ''),
        '/', '='), '=')) AS privilege
    FROM unnest(coalesce(c.relacl, ARRAY[]::aclitem[])) acl
    WHERE acl::text LIKE 'saquito=%'
) privilege_type
WHERE c.relkind = 'S'
  AND grantee.rolname = 'saquito'
ORDER BY esquema, objeto, tipo, permiso;

```
