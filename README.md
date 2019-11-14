[![Build Status](https://travis-ci.org/kugmax/udacity-scheeles-cloud-developer.svg?branch=master)](https://travis-ci.org/kugmax/udacity-scheeles-cloud-developer)

# udacity-scheeles-cloud-developer

Udacity cloud developer nanodegree [course-03](https://www.udacity.com/course/cloud-developer-nanodegree--nd9990)
Cloned from [scheeles repo](https://github.com/scheeles/cloud-developer/tree/01-start)

## Project structure
- udactiy-c3-user: authorization, authentification service; uses postgresql as db
- udacity-c3-feed: CRUD operation with photos; uses s3 as photo storage
- udacity-c3-frontend: ui presentation
- nginx: proxy between frontend-service and feed, user services

## Getting Setup

### Running using docker compose
1. Need to add config  file `scheeles.env` using `scheeles.env.example` as example.
2. Execute from project folder: `docker-compose build && docker-compose up -d`
- frontend-service url: http://localhost:8100/
- user-service url: http://localhost:8081/
- feed-service url: http://localhost:8082/

### Running the Development Serve
1. Install npm dependencies in udacity-c3-feed, udacity-c3-frontend, udactiy-c3-user `npm i`
2. Running dev server for udacity-c3-feed, udacity-c3-user `npm run dev`. Url: http://localhost:8080, because they use the same port, can be running only one of them. For udacity-c3-frontend `ionic serve` url: http://localhost:8100/

### Running Kubernetes
1. Expected that kubernetes is installed and cluster is configured.
2. Same as with docker-compose, need to add secret files. There are exaples: `...yaml.example`
3. Then apply them:
```
kubectl apply -f aws-secret.yaml
kubectl apply -f env-configmap.yaml
kubectl apply -f env-secret.yaml
```

4. Then apply services:
```
kubectl apply -f udacity-c3-feed/feed-deployment.yaml
kubectl apply -f udacity-c3-feed/feed-service.yaml
```
```
kubectl apply -f udactiy-c3-user/user-deployment.yaml
kubectl apply -f udactiy-c3-user/user-service.yaml
```
```
kubectl apply -f udacity-c3-frontend/frontend-deployment.yaml
kubectl apply -f udacity-c3-frontend/frontend-service.yaml
```
```
kubectl apply -f udacity-c3-frontend/nginx-deployment.yaml
kubectl apply -f udacity-c3-frontend/nginx-service.yaml
```
