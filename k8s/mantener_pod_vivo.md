
## DEPLOYMENT ORIGINAL
```xml
  spec:
      containers:
        - command: ["/bin/bash", "-c", "while true; do echo 'HOLA'; sleep 3600; done"]
          args:
            - "-c"
            - "config_file=/etc/postgres-conf/postgresql.conf"
          env:
            - name: POSTGRES_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: pass
                  key: K8S_POSTGRES_PASSWORD

```

## DEPLOYMENT PARA MANTENER VIVO EL POD
```xml
  spec:
      containers:
        - command: ["/bin/bash", "-c", " sleep 6000 " ]
          args: ["sleep 6000;"]
          env:
            - name: POSTGRES_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: pass
                  key: K8S_POSTGRES_PASSWORD

```
