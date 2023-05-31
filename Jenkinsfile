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
        sh 'docker build -f curriculum-front/Dockerfile -t coolnumber9/curriculum-front:latest .'
      }
    }

    stage('Log into Dockerhub') {
      environment {
        DOCKERHUB_CREDS = credentials('dockerhubaccount')
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
        sh 'echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push coolnumber9/curriculum-front:latest'
      }
    }

  }
}