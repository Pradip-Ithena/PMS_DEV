def VERSION = "${env.BUILD_NUMBER}"
def DIST_ARCHIVE = "dist.${env.BUILD_NUMBER}"
pipeline {
  agent any
  tools {
    nodejs "nodeJS"
  }
  stages {
    stage('Chekout') {
      steps {
        git branch: 'main', credentialsId: '8578e9e3-c3b9-4e6e-8ef9-c01eecff2694', url: 'https://github.com/Pradip-Ithena/PMS_DEV.git'
        echo 'Checkout Completed'
      }
    }
    stage('NPM Install') {
      steps {
        sh 'npm install'
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
          scannerHome = tool 'sonarQube';
        }
        withSonarQubeEnv('sonar') {
          sh "${scannerHome}/bin/sonar-scanner.sh"
        }
        sh 'npm run ng build'
        echo 'build Completed'
      }
    }
    stage('Archive') {
      steps {
        sh "cd dist && zip -r ../${DIST_ARCHIVE}.zip . && cd .."
        archiveArtifacts artifacts: "${DIST_ARCHIVE}.zip", fingerprint: true
        echo 'folder ziped'
      }
    }
    stage('Deploy') {
      steps {
        sh "mv ${DIST_ARCHIVE}.zip /home/ubuntu/jenkins/"
        sh "unzip /home/ubuntu/jenkins/${DIST_ARCHIVE}.zip -d /home/ubuntu/jenkins/${DIST_ARCHIVE}"
        sh "cd /home/ubuntu/jenkins/${DIST_ARCHIVE}/PMS-DEV && pm2 serve --spa . --port 4200"
        echo 'Deployed and run'
      }
    }
  }
}
