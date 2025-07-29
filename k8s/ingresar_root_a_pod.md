## No puede iniciar sesión en el pod directamente como root a través de kubectl.

Puedes hacerlo mediante los siguientes pasos.

Descubra en qué nodo se está ejecutando
```bash
kubectl get pod -n [NAMESPACE] -o wide
kubectl get pod -n postgres -o wide
```
Ingresa al nodo ssh

Encuentra el contenedor Docker
```bash
sudo docker ps | grep [namespace]
sudo docker ps | grep postgres
```
Iniciar sesión en el contenedor como root
```bash
sudo docker exec -it -u root [DOCKER ID] /bin/bash
```
