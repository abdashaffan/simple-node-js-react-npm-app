@Library('nodejs-library') _

pipeline {
    agent {
        label 'node'
    }
    environment { 
        CI = 'true'
    }
    stages {
        stage('check location') {
            steps {
                sh 'pwd'
            }
        }
        stage('check version') {
            steps {
                script {
                    version()
                }
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
