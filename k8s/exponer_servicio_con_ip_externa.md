# DAR IPS EXTERNAS

## INSTALAR 
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.10/config/manifests/metallb-native.yaml

## CREAR el ARCHIVO PARA DAR EL POOL DE CONEXION

kubectl apply -f ipaddresspool.yaml -n metallb-system

## REVISION DEL SERVICIO DE POSTGRES

Como postgres ya esta corriendo como servicio 

debo revisar en Network->services
el servicio de postgres en el item external IP ya debe dar una IP del pool
