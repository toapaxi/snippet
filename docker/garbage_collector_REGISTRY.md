# ingresar al docker de registry y ejecutar
```bash
docker exec -it registry bash
registry garbage-collect /etc/docker/registry/config.yml
```
# despues GC total
```bash
registry garbage-collect --delete-untagged /etc/docker/registry/config.yml
```
