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
    stage('Build') {
      steps {
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
        echo 'Deployed'
      }
    }
  }
}
