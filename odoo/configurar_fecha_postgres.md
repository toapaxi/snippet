# CONFIGURAR FECHA DE SERVIDOR ODOO
## EL SERVIDOR UTILIZA DMY Y NOSOTROS MDY
ABRIR EL ARCHIVO DE CONFIGURACION
/etc/postgresql/{versión}/main/postgresql.conf

En ese archivo, se busca y cambia  **datestyle = 'iso, mdy'**

**Se debe reiniciar el servicio.**
