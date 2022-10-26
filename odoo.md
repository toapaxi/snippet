# INSTALACION

## Instalar python 3.9

sudo apt install python3.9
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
pip install --upgrade pip
pip install --upgrade wheel
pip install --upgrade setuptools

## INSTALAR DEPENDIENDO DE LA VERSION DE PYTHON
sudo apt-get install python3.9-dev

## BAJAR LA VERSION DE SEPTUPTOOLS SI APARECE EL ERROR DEPRECATED SETUP Y UTILICE BUILD
pip install setuptools==58.2.0


libssl-dev

abrir el archivo requirements.txt, y procedemos a instalar

#### Actualizar PIP
python -m pip install --upgrade pip

## AL EJECUTAR POR 1RA VEZ
Salen horrores

pip install werkzeug
pip install psycopg2-binary


# ARREGLAR ODOO

SELECT id, name, description, res_model, res_field, res_id, company_id, type, url, public, access_token, db_datas, store_fname, file_size, checksum, mimetype, index_content, create_uid, create_date, write_uid, write_date, original_id
	FROM public.ir_attachment
	where store_fname like '%fdffc45cba0e31dd34423b54f06fd48e9824192c%'
	
	delete  from ir_attachment
	where id >1
	
	 select * from ir_model where model  like '%transporte.tipo%';
select * from ir_model_fields where model_id = '616';

delete from ir_model_fields where model_id = '616';

delete from ir_model where id = '616';


## BORRAR MODULOS TRUCHOS

delete from public.ir_module_module
where name like '%turnero_botate%'

DELETE FROM public.ir_model_data
where name like '%turnero_botate%'
