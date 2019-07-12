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
                version()
            }
        }
        stage('Build') {
            steps {
                script {
                    build()
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    test('./jenkins/scripts/test.sh')
                }
            }
        }
        stage('Deliver') { 
            steps {
                script {
                    deliver('./jenkins/scripts/deliver.sh')
                    input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                    terminate('./jenkins/scripts/kill.sh') 
                }
            }
        }
    }
}
