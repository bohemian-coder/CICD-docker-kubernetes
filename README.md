# Containerize and deploy a microservices application to kubernetes using KOPS

### Extending the emartapp forked from devopshydclub/emartapp

* Important Notes:

- Frontend client is based on AngularJS and is hosted on Nginx
- Backend Node API
- Backend Java API
- MongoDB Database comms with Node API
- MySQL Database comms with Java API

### Base commands

``` docker-compose build```
```docker-compose up```

Containers can be pulled directly from dockerhub :
- Node API: docker pull mkcloudpro/emartapi
- Java Web API:  docker pull mkcloudpro/emartwebapi
- AngularJS Client: docker pull mkcloudpro/emartclient
- Nginx: docker pull nginx
- MySql: docker pull mysql:8.0.33
- MongoDB: docker pull mongo