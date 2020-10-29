# Agregar servicios externos a Kubernetes

### Es necesario declarar:

* EndPoint
* Un Servicio sin selectores

Por ejemplo, para declarar una conexion a una BD externa al Cluster, como Postgres:

# Declaramos el endpoint:

```
kind: Endpoints
apiVersion: v1
metadata:
 name: postgres-db1
subsets:
 - addresses:
     - ip: 10.0.24.20
   ports:
     - port: 5432
```

Y aplicamos con:

```
kubeclt apply -f postgres-enpoint.yaml
```

# Definimos el servicio

```
kind: Service
apiVersion: v1
metadata:
  name: postgres-db1
spec:
  ports:
    -
      name: postgres-db1
      protocol: TCP
      port: 5432
      targetPort: 5432
      nodePort: 0
```

Y se aplica:

```
kubeclt apply -f postgres-external-service.yaml

```
