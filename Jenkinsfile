pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/coolnumber9/curriculum-app', branch: 'dev')
      }
    }

    stage('Print User') {
      steps {
        sh 'echo $USER'
      }
    }

    stage('Print Permission') {
      steps {
        sh 'ls -l /var/run/docker.sock'
      }
    }

    stage('Install nvm') {
      steps {
        sh '''
        apt-get install curl gnupg2 -y
        curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
        source ~/.bashrc
        nvm --version
        nvm install 16.0.0
        node --version
        '''
      }
    }

    stage('Check Node versions') {
      steps {
        sh 'nvm ls'
      }
    }

    stage('Use Node LTS v16') {
      steps {
        sh 'nvm use 16.0.0'
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