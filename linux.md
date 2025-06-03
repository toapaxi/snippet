### REVISAR ARCHIVOS PESADOS
sudo find / -type f -size +100M -exec ls -lh {} \; 2>/dev/null | awk '{ print $5, $9 }'

### BUSCAR LOS ARCHIVOS LOG PESADOS DE WILDFLY

sudo find / -type f -name "*server*log*" -printf '%s %p\n' | sort -nr | head -30

### Comprobar los certificados de un sitio web

openssl s_client -showcerts -connect gitlab.armada.mil.ec:443

### Buscar Carpetas mas pesadas
sudo find / -type d -printf '%s %p\n'| sort -nr | head -10

### Buscar Archivos mas pesados
sudo find / -type f -printf '%s %p\n'| sort -nr | head -10

### VER que puertos estan abiertos
sudo lsof -i -P -n | grep LISTEN | grep IPv4

### Cuando estoy instalando algo y se corta porque me dice que faltan librerias
Ejecuto lo siguinete, para que instale las librerias faltantes y continue 
sudo apt-get install -f

### Liberar Memoria 
```
sudo sh -c 'echo 3 > /proc/sys/vm/drop_caches'
```
