### Comprobar los certificados de un sitio web

openssl s_client -showcerts -connect gitlab.armada.mil.ec:443

### Buscar Carpetas mas pesadas
sudo find / -type d -printf '%s %p\n'| sort -nr | head -10

### Buscar Archivos mas pesados
sudo find / -type f -printf '%s %p\n'| sort -nr | head -10

### VER que puertos estan abiertos
sudo lsof -i -P -n | grep LISTEN | grep IPv4
