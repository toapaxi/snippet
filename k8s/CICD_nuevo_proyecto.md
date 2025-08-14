# Configuracion CI/CD de un proyecto nuevo

# creacion del RUNNER en GITLAB

PROYECTO--> CI/CD Settings-->New runner

Dar clic en *Create runner*

<img width="545" height="662" alt="image" src="https://github.com/user-attachments/assets/4d5759d6-dd17-47d8-90b4-15149cb3728a" />

Nos indicara la creacion del runner
```bash
gitlab-runner register  --url https://gitlab.armada.mil.ec  --token glrt-t3_i3FFKUEVLz3TFLgZWAyx
```
# Crear el runner en GITLAB-RUNNER
## Ingresar en el docker con GITLAB-RUNNER
docker exec -it runner bash
## ejecutar la creacion del runner
```bash
gitlab-runner register  --url https://gitlab.armada.mil.ec  --token glrt-t3_i3FFKUEVLz3TFLgZWAyx
```
Debemos ingresar el nombre del runner *hola*
<img width="1274" height="368" alt="image" src="https://github.com/user-attachments/assets/1207b5a8-a08a-4dd1-a29a-0a9df8f42351" />
