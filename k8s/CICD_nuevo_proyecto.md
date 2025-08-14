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
Debemos ingresar el nombre del runner **webspoon-olap** y el ejecutor sera **shell**
<img width="1274" height="368" alt="image" src="https://github.com/user-attachments/assets/1207b5a8-a08a-4dd1-a29a-0a9df8f42351" />

# actualizar gitlab-ci.yml cambiar el runner_tag
```xml
RUNNER_TAG: webspoon-olap
```
# Cambiar las ramas a PROTECTED

la rama develop/staging/main, deben estar protegidas porque sino no puede ver las variables de group

# Creacion de TOKEN para deploy
Con estos valores se debe crear una variable de CI/CD
<img width="1305" height="725" alt="image" src="https://github.com/user-attachments/assets/2445847b-4ff1-409b-870f-2b15f4b9fdad" />

# Creacion de variable de CI/CD
## Para el Usuario
<img width="336" height="689" alt="image" src="https://github.com/user-attachments/assets/a63fe59b-ad9d-458a-b232-6194305c4ad8" />


## Para el TOKEN
<img width="344" height="682" alt="image" src="https://github.com/user-attachments/assets/2b89a270-530c-45b8-9e0d-da159b86845b" />

