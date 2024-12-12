# ESCOGER EL ENTORNO RESPECTIVO

```bash
kubeselect
```

## INGRESAMOS AL ROL DEL ENTORNO

```bash
cd clusters-roles/roles_staging/roles/
```

## Creamos el SA del proyecto que necesitamos

```bash
kubectl apply -f intranet.yaml -n intranet
```

### Para desarrollo tenemos otro ejemplo

```bash
cd /home/muerte/proyectos/clusters-roles/roles_develop/roles/
kubectl apply -f intranet.yaml -n intranet
```

# OBTENER EL TOKEN para copiarlo en gitlab

```bash
bash get-credential webspoon
```

copiar ese resultado en la variable KUBE_TOKEN del proyecto correspondiente
