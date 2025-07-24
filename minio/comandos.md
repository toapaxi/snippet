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
