pipeline {
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/XXXXXXXXXXXXXX.git', branch: 'master', credentialsId: 'XXXXXXXX-github-user-token'])
      }
    }
    stage('Building the app') {
      steps{
        script {
          sh 'docker-compose up'
        }
      }
    } 
}
