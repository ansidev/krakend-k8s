# krakend-k8s

## Prerequisites

- minikube.
- Read the original tutorial https://www.krakend.io/blog/krakend-on-kubernetes/

## Command notes

Run
```shell
minikube start
```

Run this command in a separate terminal
```
minikube dashboard
```

## Building the Docker images

### Build Back-end API Docker image

```shell
cd backend
```

```shell
eval $(minikube docker-env)
```

```shell
docker build -t fake-api -f Dockerfile .
```

### Build KrakenD Docker image

```shell
docker images
```

```shell
docker build -t k8s-krakend:0.0.2 .
```

## Deploying in kubernetes
### Deploy the backend API in k8s

```
kubectl run fake-api --image=fake-api:latest --port=8080 --image-pull-policy='Never'
```

```shell
kubectl expose deployment fake-api --type=NodePort
```

### Deploy the API gateway in k8s

```shell
kubectl create -f deployment-definition.yaml
```

```shell
kubectl create -f service-definition.yaml
```

## Testing the services

### Expose the service to the host

```shell
kubectl port-forward services/krakend-service 8000:8000
```
