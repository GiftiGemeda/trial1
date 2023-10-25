pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('gifti-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t gifti/example:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push gifti/example:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
