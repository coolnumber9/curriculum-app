pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/coolnumber9/curriculum-app', branch: 'dev')
      }
    }

    stage('Log') {
      steps {
        sh 'ls -la'
      }
    }

    stage('Build') {
      steps {
        sh 'sudo docker build -f curriculum-front/Dockerfile -t coolnumber9/curriculum-front:latest .'
      }
    }

    stage('Log into Dockerhub') {
      environment {
        DOCKERHUB_CREDS = credentials('dockerhubaccount')
      }
      steps {
        sh 'echo $DOCKERHUB_CREDS_PSW | sudo docker login -u $DOCKERHUB_CREDS_USR --password-stdin'
      }
    }

    stage('Push') {
      steps {
        sh 'sudo docker push coolnumber9/curriculum-front:latest'
      }
    }

  }
}