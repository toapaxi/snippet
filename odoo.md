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


# ARREGLAR ODOO (FileNotFoundError: [Errno 2] No existe el archivo o el directorio:)
## '/home/muerte/.local/share/Odoo/filestore/conaplas16/2f/2f7028932480cdcb927f83b0165d577669e620fa'

select * from ir_attachment
WHERE
store_fname LIKE '%b8f9001425cfd0ef0315797909281b912817643a%'

Confirmamos la existencia de ese registro y lo borramos

delete from ir_attachment
WHERE
store_fname LIKE '%b8f9001425cfd0ef0315797909281b912817643a%'


select * from ir_model where model  like '%transporte.tipo%';

select * from ir_model_fields where model_id = '616';

delete from ir_model_fields where model_id = '616';

delete from ir_model where id = '616';


## BORRAR MODULOS TRUCHOS

delete from public.ir_module_module
where name like '%turnero_botate%'

DELETE FROM public.ir_model_data
where name like '%turnero_botate%'
