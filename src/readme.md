# Manifests Deployment

### helm repo
```sh
helm repo add apache-airflow https://airflow.apache.org
helm repo add elastic https://helm.elastic.co
helm repo update
```

### minio [deepstorage]
```shell
kubectl apply -f app-manifests/deepstorage/minio-operator.yaml
kubectl apply -f app-manifests/deepstorage/minio-tenant.yaml
```

### hive metastore [metastore]
```shell
kubectl apply -f app-manifests/metastore/hive-metastore.yaml
```

### trino [warehouse]
```shell
kubectl apply -f app-manifests/warehouse/trino.yaml
```

### airflow [orchestrator]
```shell
kubectl create namespace orchestrator

kubectl create secret generic airflow-fernet-key --from-literal=fernet-key='cnJMV0FrY2lvQkxIeUFBMEItcE13MzhWNnFyX082aVcxVTBjZ21jSzlVbz0K' --namespace orchestrator

kubectl apply -f git-credentials-secret.yaml --namespace orchestrator
```



