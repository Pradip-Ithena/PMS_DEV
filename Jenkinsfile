pipeline {
  agent any
  tools {
    nodejs "nodeJS"
  }
  stages {
    stage('Chekout') {
      steps {
        git branch: 'main', credentialsId: 'df639a56-04b5-408d-b7ad-995f87f75ab6', url: 'https://github.com/Pradip-Ithena/PMS_DEV.git'
        echo 'Checkout Completed'
      }
    }
    stage('NPM Install') {
      withEnv(["NPM_CONFIG_LOGLEVEL=warn"]) {
        sh 'npm install'
        sh 'npm install http-server'
      }
    }
    stage('Test') {
      steps {
        echo 'test Completed'
      }
    }
    stage('Build') {
      steps {
        sh 'ng build --prod'
        echo 'build Completed'
      }
    }
    stage('Deploy') {
      steps {
        sh 'ng serve --host 192.168.1.41 --port 8081'
      }
    }
  }
}
