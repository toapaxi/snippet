# ingresar en la rama del desarrollador
```bash
git checkout nombre_rama
```
# ver los commit
```baah
git log --oneline
```
# si son 3 commit que se van a unir
```bash
git rebase -i HEAD~3
```
# se abre un archivo de configuracion 
```bash
pick a1b2c3 Mensaje del commit más antiguo
pick d4e5f6 Otro commit
pick g7h8i9 Último commit
```

# y se cambia a squash cuando los quiera unificar
```bash
pick a1b2c3 Mensaje del commit más antiguo
squash d4e5f6 Otro commit
squash g7h8i9 Último commit
```
# y guardo los cambios
```bash
git push -f
```
