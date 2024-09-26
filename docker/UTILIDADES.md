# ver el archivo log de un contenedor
```bash
docker inspect --format='{{.LogPath}}' nombre_del_contenedor
```
# truncar los logs de los container
En el docker-compose agregar al final del contenedor
```xml
  logging:
       driver: "json-file"
       options:
           max-size: "200M"
           max-file: "10"

```
