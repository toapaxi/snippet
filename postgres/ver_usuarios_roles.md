# VER LOS USUARIOS Y ROLES DE LA BASE

```psql
-- USUARIOS Y ROLES 

WITH RECURSIVE roles_heredados(usuario, rol_asignado) AS (
    -- Roles directos
    SELECT u.rolname, r.rolname
    FROM pg_roles u
    LEFT JOIN pg_auth_members m ON m.member = u.oid
    LEFT JOIN pg_roles r ON r.oid = m.roleid
    WHERE u.rolcanlogin

    UNION

    -- Roles indirectos (herencia)
    SELECT rh.usuario, r2.rolname
    FROM roles_heredados rh
    JOIN pg_auth_members m2 ON m2.member = (SELECT oid FROM pg_roles WHERE rolname = rh.rol_asignado)
    JOIN pg_roles r2 ON r2.oid = m2.roleid
)
SELECT DISTINCT usuario, rol_asignado
FROM roles_heredados
ORDER BY usuario, rol_asignado;
```
