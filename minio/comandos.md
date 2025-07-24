## DEBE TENER INSTALADO EL MINIO CLIENTE

## ✅ 1. Configura el nuevo MinIO en mc
```bash
mc alias set minio-des https://minio-api-des.armada.mil.ec minio-admin password
```
## ✅ 2. Crea los buckets (si no existen)
```bash
for d in */ ; do
  bucket=$(basename "$d")
  mc mb minio-des/"$bucket"
done
```

## ✅ 3. Sube el contenido al nuevo MinIO
```bash
for d in */ ; do
  mc cp --recursive "$d" minio-des/"$(basename "$d")"
done
```

## ✅ 4. Elimina todos los buckets con un solo comando
```bash
for bucket in $(mc ls minio-des | awk '{print $NF}'); do
  mc rm --recursive --force minio-des/"$bucket"
  mc rb minio-des/"$bucket"
done
```
## Borrar
```bash
# borra todo el contenido del bucket vpn
  mc rm --recursive --force myminio/vpn
# borra bucket vpn
  mc rb myminio/vpn
# crea bucket vpn
  mc mb myminio/vpn
# copia de mi carpeta hacia el bucket vpn
  mc cp --recursive ./vpn myminio/vpn
```
