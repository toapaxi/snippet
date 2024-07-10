# Ingreso via psql

psql -U postgres

## ejecuto el comando

show config_file;
vi /var/lib/postgresql/data/postgresql.conf

## VER TODOS LOS QUERYS

CHANGE LOGS OFF TO ON
logging_collector = on 
log_directory = 'log'  
log_filename

show log_statemens

log_statemens 'all'
