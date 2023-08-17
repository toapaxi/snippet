# INSTALACION

## Instalar python 3.9
```console
sudo apt install python3.9
```
## Descargar 

Descargar desde la carpeta src la ultima version
https://nightly.odoo.com/15.0/nightly/

descomprimir en cualquier carpeta
crear los archivos odoo-server y odoo.conf

### Crear una nueva Run/Debug Configurations
Name: odoo-server
Script Path:  /home/muerte/proyectos/ODOO_SRC_15/odoo-server
Parameters:   -c /home/muerte/proyectos/ODOO_SRC_15/odoo.conf
Working directory:  /home/muerte/proyectos/ODOO_SRC_15

Lo demas por default


### Instalar requerimientos
#### Actualizar Python
```console
pip install --upgrade pip
pip install --upgrade wheel
pip install --upgrade setuptools
```
## INSTALAR DEPENDIENDO DE LA VERSION DE PYTHON
```console
sudo apt-get install python3.9-dev
```
## BAJAR LA VERSION DE SEPTUPTOOLS SI APARECE EL ERROR DEPRECATED SETUP Y UTILICE BUILD
```console
pip install setuptools==58.2.0

```
libssl-dev

abrir el archivo requirements.txt, y procedemos a instalar

#### Actualizar PIP
```console
python -m pip install --upgrade pip
```
## AL EJECUTAR POR 1RA VEZ
Salen horrores
```console
pip install werkzeug
pip install psycopg2-binary
```

## BORRAR MODULOS TRUCHOS
```sql
delete from public.ir_module_module
where name like '%turnero_botate%'

DELETE FROM public.ir_model_data
where name like '%turnero_botate%'
```

# BUSCAR CATEGORIAS Y GRUPOS DE USUARIOS
```sql
SELECT *
FROM ir_module_category
WHERE to_json(name)::text LIKE '%nomina%';
```
## Luego podemos buscar en la tabla res_groups
```sql
SELECT * FROM res_groups
WHERE category_id = 89
to_json(name)::text LIKE '%Usuario%';
```
