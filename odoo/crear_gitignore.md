# Crear archivo .gitignore

Contenido del archivo .gitignore
``` bash
# Python files

*.pyc
__pycache__/

# GitLab

.gitlab/
```

# EJECUTAR EN EL PATH RAIZ DE CADA PROYECTO


Elimina los archivos almacenados en GIT

``` bash
git rm -r --cached *.pyc
git rm -r --cached __pycache__
``` 
