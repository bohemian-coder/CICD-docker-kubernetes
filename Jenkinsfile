pipeline {
    agent any
    environment {
      clientRegistry = "mkcloudpro/emartclient"
      webapiRegistry = "mkcloudpro/emartwebapi"
      apiRegistry = "mkcloudpro/emartapi"
      registryCredential = 'dockercredential'
    }
    stages {
        // stage('Test') {
        //     // Run tests for each microservice
        // }
        stage('Build images in docker-compose.yml') {
            steps {
              sh "docker-compose build"
              //dockerComposeBuild(buildComposeFile: 'docker-compose.yml')
            }
        }
        stage('Push images to docker hub') {
            steps {
              script {
                docker.withRegistry('', registryCredential){
                  sh 'docker-compose push'
                }
              }
            }
        }
        stage('Remove images post push') {
          steps{
            sh """
            docker rmi \$(docker image ls | grep mkcloudpro | awk '{print \$3}')
            """
          }
        }
        stage ('Kubernetes Deploy using Helm'){
          agent {label 'kops'}
          steps {
            sh "helm upgrade --install --namespace emartprod -f helm/emartcharts/values.yml emartapp-stack helm/emartcharts"
          }
        }
    }
}
