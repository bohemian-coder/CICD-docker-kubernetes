# Containerize and deploy a microservices application to kubernetes using KOPS

### Extending the emartapp forked from devopshydclub/emartapp, to include Kubernetes orchestration on AWS

#### System Requirements (Local / Cloud)
The *scripts* folder has all the pre-reqs needed for your "local" machine. Setup for Ubuntu Focal 20.4, but should run on 18 and 22+
- Docker
- Kubectl
- Kops
- awscli
- if using an EC2 instance; t3 medium is recommended


#### Docker Requirements

To create your own images and run the app w/out kubernetes:
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
- A registered domain name is required for your cluster
- Cluster should have at least 2 worker nodes and 1 master node to avoid pod evictons. Use *KopsCmds* as a guide for cluster setup.
- All relevant declaration files are contained in *kube-app* folder.
- Configs use ContainerInit to force a deployment order, you can do this manually following this order;
MySQL DB -> MongoDB -> NodeAPI -> WebAPI -> Client -> Nginx

To run configs and setup pods, services, configmaps, persistent-volumes & PV claims:
```kubectl apply -f <filename>```

#### warning:
- This is not secure enough for a production env : please use secret keys for all passwords.

- If running this on AWS, there will be some charges as it is not completely free tier compatible