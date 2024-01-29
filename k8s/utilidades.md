# K8S

## INGRESAR CON BASH A UN POD

```bash
kubectl exec -it  pods/minio-6f47b68c96-xcmgw sh  -n minio
```

## COPIAR DE LOCAL A POD
```bash
kubectl cp Pritunl.exe  minio-6f47b68c96-xcmgw:/data/vpn  -n minio
```
