pipeline {
  agent any
  tools {
    nodejs "nodeJS"
  }
  stages {
    stage('Chekout') {
      steps {
        git branch: 'main', credentialsId: '9cc6dcda-ec9f-4b57-939b-9985d0298570', url: 'https://github.com/Pradip-Ithena/PMS_DEV.git'
        echo 'Checkout Completed'
      }
    }
    stage('NPM Install') {
      steps {
        sh 'npm install'
        sh 'npm install http-server'
        echo 'installation Completed'
      }
    }
    stage('Test') {
      steps {
        echo 'test Completed'
      }
    }
    stage('Build') {
      steps {
        sh 'npm run ng build'
        echo 'build Completed'
      }
    }
    stage('Deploy') {
      steps {
        sh 'npm run ng serve --host 192.168.1.41 --port 8081'
      }
    }
  }
}
