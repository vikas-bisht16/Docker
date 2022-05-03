pipeline {
  agent any
  stages {
    stage('Building the app') {
      steps{
        script {
          sh 'docker-compose up'
        }
      }
    } 
  }
}
