# Deploy Nest App with Docker + Kubernettes on google Cloud

[Nest](https://github.com/nestjs/nest) framework TypeScript starter repository.

## Create nest project

```bash
$ nest new my-project
```

## Create a docker Image

- Create Dockerfile

- In docker hub create a new repository

- Login to the repository from bash

```bash
docker login
```

- Build the image with the repository name

```bash
docker build -t zoutigo/nestjs-k8s .
```

- push the image

```bash
docker push zoutigo/nestjs-k8s
```

## Kubernettes

- start minikube

```bash
$ minikube start
```

- create a k8s folder
  container port same as the one in the app

- create a deployment.yaml
  Image must be the one built previously in docker hub

- create a deployment

```bash
kubectl create -f deployment.yaml
```

- check the created pods

```bash
kubectl get pods
```

- check the pods logs

```bash
kubectl logs <podname>
```

- create a service.yaml
  this for the pod to communicate

- Create service

```bash
kubectl create -f service.yaml
```

- check created service

```bash
kubectl get svc
```

- get the service url

```bash
minikube service nestjs-k8s --url
```

## Déployer sur Gcloud

- créer un projet
  [https://console.cloud.google.com/kubernetes/list/] lien google

- activer l'api

- créer le service en autopilote GKE

- installer cloud sdk
  [https://cloud.google.com/sdk/docs/install-sdk#deb] Lien de la procedure

- initialiser gcloud

```bash
gcloud init
```

- Demarrer Gcloud en se connectant grace au lien obtenu , dans connecter sur la plateform

```bash
gcloud container clusters get-credentials autopilot-cluster-1 --region europe-west1 --project nestjs-k8s-354706
```

- tester si on peut y utiliser kubectl

```bash
kubectl get namspaces
```

- Mettre Loadbalancer
  Dans service.yaml , mettre le type à LoadBalancer

- Créer le deployment et le service
  Se mettre dans le repertoire k8s

```bash
kubectl create -f .
```

- Vérifier les pods créés

```bash
kubectl get pods
```

- Lister les services

```bash
kubectl get svc
```

Dans notre service nestjs-k8s , on a
external ip : 34.79.176.52
ports : 3000:31802/TCP

l'url à requetter est donc 34.79.176.52:3000

$ npm run start:dev

# production mode

$ npm run start:prod

````

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
````

## Support

Nest is an MIT-licensed open source project. It can grow thanks to the sponsors and support by the amazing backers. If you'd like to join them, please [read more here](https://docs.nestjs.com/support).

## Stay in touch

- Author - [Kamil Myśliwiec](https://kamilmysliwiec.com)
- Website - [https://nestjs.com](https://nestjs.com/)
- Twitter - [@nestframework](https://twitter.com/nestframework)

## License

Nest is [MIT licensed](LICENSE).
