pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/yourusername/devops-sample-project.git'
      }
    }
    stage('Build') {
      steps {
        sh 'docker build -t yourdockerhubusername/devops-sample-app .'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run --rm yourdockerhubusername/devops-sample-app npm test'
      }
    }
    stage('Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
          sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
          sh 'docker push yourdockerhubusername/devops-sample-app'
        }
      }
    }
  }
}

