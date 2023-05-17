
# AGREGAR SSH KEY A GITLAB

## Generamos un nuevo TOKEN 

Este token permite autorizar el envio de informacion entre el PC/laptop hacia el servidor.
Realice los siguientes pasos:
1. Abrir un terminal
2. EJECUTAR ssh-keygen -t rsa -b 2048 -C "LAPTOP-DEL-TRABAJO"
3. dar next, next, next
4. EJECUTAR cat ~/.ssh/id_rsa.pub
Y se mostrara un texto como el siguiente (Inicia con ssh-rsa):
**ssh-rsa** AAAAB3NzaC1yc2EAAAADAQABAAABAQDRgdNd6n39d3HMx7dGaKO7x/zS64EsWyVZ7mWS6WPLzHbDV13tS9e7CYGIGfxQP5EBPNpoVrM3rsOo5QGRuCJVqXY/YuCiWrKjeZOqLOBvXNXmzZI8rrSyxnhXJ892OV+63+AqCTN+PYXD5X/0IIIChyRYxE7QFzk2k7r9ZDZC2nAjp17ipMouItjcunmaEMTniyPpXwZ0P0ENe0N3nLFK/zLS8YIxx0rSVDGxJgkO5ruCdJlO882LHLv80+Afsuhpe0HtTnFTvyPKfvHbsbw7afwdql5wNZk0aBqmWHuCufhQvMaUkQ8RPw7VyKfT6UXYo5eRpBYgXfxMold2R4fL dirtic-ctoapaxi
5. copiar 

## Configuramos en GITLAB
En el menu de Usuario ingresar en User Setting --> SSH Keys se configura el TOKEN nuevo que vamos a generar
1. En el campo key copiamos el item 5 anterior
2. En el campo key coloque una descripcion de la PC que esta configurando.
3. Dar clic en **Add key**
