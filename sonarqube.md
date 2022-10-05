## Error al instalar en UBUNTU
### bootstrap check failure [1] of [1]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]

Me pide cada vez que reinicio ubuntu
Solución: sudo sysctl -w vm.max_map_count=262144

### Clave por default
usuario: admin
clave: admin


### Conectarme con gitlab

* nombre cualquiera
* Usar la URL por default https://gitlab.armada.mil.ec/api/v4
* Colocar el token personal
