# Containerize and deploy a microservices application to kubernetes using KOPS

### Extending the emartapp forked from devopshydclub/emartapp, to include Kubernetes deployment on AWS

#### Notes:

- Frontend client is based on AngularJS and is hosted on Nginx
- Backend Node API
- Backend Java API
- MongoDB Database comms with Node API
- MySQL Database comms with Java API

#### System Requirements
The *scripts* folder has all the pre-reqs needed. It is setup for Ubuntu Focal 20.4, but should run on 18 and 22+
- Docker
- Kubectl
- Kops
- awscli

#### Docker Requirements

``` docker-compose build```
```docker-compose up```

Containers can be pulled directly from dockerhub :
- Node API: docker pull mkcloudpro/emartapi
- Java Web API:  docker pull mkcloudpro/emartwebapi
- AngularJS Client: docker pull mkcloudpro/emartclient
- Nginx: docker pull nginx
- MySql: docker pull mysql:5.6
- MongoDB: docker pull mongo

#### K8s Requirements
The *kube-app* folder contains all k8s config files
Use *KopsCmds* to set up a 2 - 3 node cluster on AWS

Configs use ContainerInit to force a deployment order;
Deployment order: MySQL DB -> MongoDB -> NodeAPI -> WebAPI -> Client -> Nginx