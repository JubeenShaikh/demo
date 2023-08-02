pipeline {
    agent any 
      stages {
        stage('build maven instalation'){
          steps {
            sh 'pwd'
            sh 'mvn clean install package'
          }
        }
        stage('copy artifacts'){
          steps {
            sh 'pwd'
            sh 'cp -r target/*.jar docker'
          }
        }
        stage('run test'){
          steps {
            sh 'mnv test'
          }
        }
        stage('build docker image'){
          steps {
            script {
              def custoImage = docker.build("jubeenshaikh/petclinic:${env.BUILD_NUMBER}", "./docker")
              docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
              customeImage.push()
            }
          }
        }
        stage('buil on k8s'){
          steps {
            withKubeConfig([credentialsId: 'kubeconfig']){
              sh 'pwd'
              sh 'cp -R helm/* .'
              sh 'ls -ltrh'
              sh 'pwd'
              sh '/usr/local/bin/helm upgrade --install petclinic-app petclinic --set image.repository=jubeenshaikh/petclinic --set image.tag=${BUILD_NUMBER}'
            }
          }
        }
