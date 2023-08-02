pipeline {
    agent any 
      stages {
        stage('build maven instalation'){
          steps {
            sh 'pwd'
            sh 'mvn clean install package'
          }
        }
      }
}
