pipeline {
  agent any
  tools {
    nodejs "nodeJS"
  }
  stages {
    stage('Chekout') {
      steps {
        git branch: 'main', url: 'https://github.com/Pradip-Ithena/PMS_DEV.git'
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
    stage('Build + SonarQube analysis') {
      steps {
        script {
            scannerHome = tool 'SonarQube Scanner';
        }
        withSonarQubeEnv('sonar') {
            sh "${scannerHome}/bin/sonar-scanner.sh" 
        }
        sh 'npm run ng build'
        echo 'build Completed'
      }
    }
    stage('Deploy') {
      steps {
        sh 'npm run ng serve --host 65.2.163.29 --port 4201'
        echo 'running state'
      }
    }
  }
}
