pipeline {
    agent any
    tools { nodejs "nodeJS" }

    stages {
        stage('NPM Install') {
            steps {
                script {
                    notifyBitbucket(buildStatus: 'INPROGRESS')
                }
                sh 'npm install'
                sh 'npm install http-server'
            }
        }
        stage('Test') {
            steps {
                sh 'ng test'
            }
        }
        stage('Build') {
            steps {
                sh 'ng build --prod'
            }
        }
        stage('Deploy') {
            steps {
                sh 'ng serve --host 192.168.1.41 --port 8081'
            }
        }
    }
}