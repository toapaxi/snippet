# Cambiar certificados ssl

## Certificados que nos envian
La unidad certificadora envia 3 archivos

- web01.key
- DigiCertCA.crt
- star_armada_mil_ec.crt

## Crear archivos 

### Clave Privada

```bash
cp web01.key armada.key
```
### Clave Completa

```bash
cat star_armada_mil_ec.crt DigiCertCA.crt > armada.crt
cat star_armada_mil_ec.crt DigiCertCA.crt > fullchain.crt
```

## Reemplazar en el servidor NGINX

Se debe buscar el path de NGINX, por ejemplo

/home/gitlab/nginx/certs

se copia los archivos generados.

## Reiniciar el servidor NGINX (DOCKER)

```bash
docker exec nginx nginx -s reload

docker exec nginx nginx -t

```
