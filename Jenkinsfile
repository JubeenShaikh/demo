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
            sh 'mvn test'
          }
        }
        stage('build docker image'){
          steps {
            script {
              def customImage = docker.build("jubeenshaikh/petclinic:${env.BUILD_NUMBER}", "./docker")
              docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
              customeImage.push()
            }
          }
        }
      }
}
