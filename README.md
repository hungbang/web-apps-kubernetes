# Deployments of Angular, React and Vue Applications on Kubernetes

This project describes how to deploy Angular, React and Vue applications to Kubernetes on the IBM Cloud.


**Prerequisites**

Make sure you have the following tools installed:

* [Node](https://nodejs.org/en/download/)
* [Docker](https://docs.docker.com/engine/installation/)
* [Kubernetes CLI](https://kubernetes.io/docs/user-guide/prereqs/)
* [git](https://git-scm.com/downloads)
* For deployments to Kubernetes on the IBM Cloud: [Create Account](https://console.bluemix.net/registration/)
* For deployments to Kubernetes on the IBM Cloud: [IBM Cloud CLI](https://clis.ng.bluemix.net/)
* For Angular: [Angular CLI](https://github.com/angular/angular-cli)
* For React: [React CLI](https://github.com/facebook/create-react-app)
* For Vue: [Vue CLI](https://github.com/vuejs/vue-cli)

Clone the repo:

```sh
$ git clone https://github.com/nheidloff/web-apps-kubernetes.git
```


## Angular

Create a new application or use the provided sample application which has been generated with the Angular CLI:

```sh
$ npm install -g @angular/cli
$ ng new angular-app
$ cd angular-app
$ ng build --prod
```

Run the application locally:

```sh
$ cd web-apps-kubernetes/angular-app
$ npm install
$ ng serve
```

Build the Docker image:

```sh
$ cd web-apps-kubernetes/angular-app
$ docker build -t angular-app .
```

Run Docker container locally:

```sh
$ cd web-apps-kubernetes/react-app
$ docker run -d -p 8080:80 react-app 
```

Push the Docker image to the IBM Cloud Image Registry (replace the namespace/account):

```sh
$ bx plugin install container-service -r Bluemix
$ bx login -a https://api.ng.bluemix.net
$ bx cs region-set us-south
$ bx cr login
$ docker tag angular-app registry.ng.bluemix.net/nheidloff/angular-app
$ docker push registry.ng.bluemix.net/nheidloff/angular-app
```

Or push it to DockerHub (replace the namespace/account):

```sh
$ docker login
$ docker tag angular-app nheidloff/angular-app
$ docker push nheidloff/angular-app
```

Deploy the application to Kubernetes on the IBM Cloud:

Change the Docker image name in [kube-angular.yaml](angular/kube-angular.yaml). By default an image is used from DockerHub.

```sh
$ bx plugin install container-service -r Bluemix
$ bx login -a https://api.ng.bluemix.net
$ bx cs region-set us-south
$ bx cs clusters
$ bx cs cluster-config <your-cluster-name>
$ export ... (copy the output of previous command)
$ kubectl apply -f kube-angular.yaml
```

Open the application:

```sh
$ bx cs workers <your-cluster-name>
$ kubectl describe service angular-app
```

Copy the public IP address of your cluster and the NodePort, e.g. 33838, and open the app in a browser.


## React

Create a new application or use the provided sample application which has been generated with the React CLI:

```sh
$ npm install -g create-react-app
$ create-react-app react-app
$ cd react-app
$ npm run build
```

Run the application locally:

```sh
$ cd web-apps-kubernetes/react-app
$ npm start
```

Build the Docker image:

```sh
$ cd web-apps-kubernetes/react-app
$ docker build -t react-app .
```

Run Docker container locally:

```sh
$ cd web-apps-kubernetes/react-app
$ docker run -d -p 8080:80 react-app 
```

Push the Docker image to the IBM Cloud Image Registry (replace the namespace/account):

```sh
$ bx plugin install container-service -r Bluemix
$ bx login -a https://api.ng.bluemix.net
$ bx cs region-set us-south
$ bx cr login
$ docker tag react-app registry.ng.bluemix.net/nheidloff/react-app
$ docker push registry.ng.bluemix.net/nheidloff/react-app
```

Or push it to DockerHub (replace the namespace/account):

```sh
$ docker login
$ docker tag react-app nheidloff/react-app
$ docker push nheidloff/react-app
```

Deploy the application to Kubernetes on the IBM Cloud:

Change the Docker image name in [kube-react.yaml](angular/kube-react.yaml). By default an image is used from DockerHub.

```sh
$ bx plugin install container-service -r Bluemix
$ bx login -a https://api.ng.bluemix.net
$ bx cs region-set us-south
$ bx cs clusters
$ bx cs cluster-config <your-cluster-name>
$ export ... (copy the output of previous command)
$ kubectl apply -f kube-react.yaml
```

Open the application:

```sh
$ bx cs workers <your-cluster-name>
$ kubectl describe service react-app
```

Copy the public IP address of your cluster and the NodePort, e.g. 33838, and open the app in a browser.


## Vue

Create a new application or use the provided sample application which has been generated with the Vue CLI:

```sh
$ npm install --global vue-cli
$ vue init webpack vue-app
$ cd vue-app
$ npm run build
```

Run the application locally:

```sh
$ cd web-apps-kubernetes/vue-app
$ npm run dev
```

Build the Docker image:

```sh
$ cd web-apps-kubernetes/vue-app
$ docker build -t vue-app .
```

Run Docker container locally:

```sh
$ cd web-apps-kubernetes/vue-app
$ docker run -d -p 8080:80 vue-app 
```

Push the Docker image to the IBM Cloud Image Registry (replace the namespace/account):

```sh
$ bx plugin install container-service -r Bluemix
$ bx login -a https://api.ng.bluemix.net
$ bx cs region-set us-south
$ bx cr login
$ docker tag vue-app registry.ng.bluemix.net/nheidloff/vue-app
$ docker push registry.ng.bluemix.net/nheidloff/vue-app
```

Or push it to DockerHub (replace the namespace/account):

```sh
$ docker login
$ docker tag vue-app nheidloff/vue-app
$ docker push nheidloff/vue-app
```

Deploy the application to Kubernetes on the IBM Cloud:

Change the Docker image name in [kube-vue.yaml](angular/kube-vue.yaml). By default an image is used from DockerHub.

```sh
$ bx plugin install container-service -r Bluemix
$ bx login -a https://api.ng.bluemix.net
$ bx cs region-set us-south
$ bx cs clusters
$ bx cs cluster-config <your-cluster-name>
$ export ... (copy the output of previous command)
$ kubectl apply -f kube-vue.yaml
```

Open the application:

```sh
$ bx cs workers <your-cluster-name>
$ kubectl describe service vue-app
```

Copy the public IP address of your cluster and the NodePort, e.g. 33838, and open the app in a browser.