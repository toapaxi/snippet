
# Cambiar el id de un grupo de usuario
Si deseamos cambiar el id de un res_group 

        <record id="grupo_usuario_nm" model="res.groups">
            <field name="name">Usuario de Nominas</field>
            <field name="category_id" ref="nm_security"/>
        </record>
        <record id="grupo_usuario_nm" model="res.groups">
            <field name="name">Usuario de Nominas</field>
            <field name="category_id" ref="nm_security"/>
        </record>
        
## Debemos cambiarlo en la base de datos

### Buscar el registro
        SELECT *
        FROM ir_module_category
        WHERE to_json(name)::text LIKE '%nomina%';

        SELECT * FROM res_groups
        WHERE category_id = 89
        and to_json(name)::text LIKE '%Usuario%';
        --El id es 119

        --Lo puedes puscar por id
        select module, name, * from ir_model_data 
        where model = 'res.groups'
        and res_id = 119

        --Tambien lo puedes puscar por nombre
        select * from ir_model_data 
        where model = 'res.groups'
        and module = 'nm_accesos'
        and name = 'grupo_user_nm'

### Actualizar el campo name del registro en la tabla ir_model_data
        begin
        update ir_model_data set name = 'grupo_usuario_nm'
        where model = 'res.groups'
        and res_id = 119
        rollback
        commit 

# DESPUES DEBEMOS MODIFICAR TODAS LAS REFERENCIAS EN EL CODIGO
BUSCAR: nm_accesos.grupo_user_nm
Y REEMPLAZAR POR: nm_accesos.grupo_usuario_nm

        modified:   corp_hr_catalogos/security/ir.model.access.csv
        modified:   corp_hr_catalogos/views/corp_menu.xml
        modified:   nm_catalogos/security/ir.model.access.csv
        modified:   th_empleados/security/ir.model.access.csv

