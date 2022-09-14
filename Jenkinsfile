pipeline {
  agent any
  tools {
    nodejs "nodeJS"
  }
  stages {
    stage('Chekout') {
      steps {
        git branch: 'main', credentialsId: 'df639a56-04b5-408d-b7ad-995f87f75ab6', url: 'https://github.com/Pradip-Ithena/PMS_DEV.git'
      }
    }
    stage('NPM Install') {
      steps {
        execCmd 'npm install'
        execCmd 'npm install http-server'
      }
    }
    stage('Test') {
      steps {
        execCmd 'test Completed'
      }
    }
    stage('Build') {
      steps {
        execCmd 'ng build --prod'
      }
    }
    stage('Deploy') {
      steps {
        execCmd 'ng serve --host 192.168.1.41 --port 8081'
      }
    }
  }
}
