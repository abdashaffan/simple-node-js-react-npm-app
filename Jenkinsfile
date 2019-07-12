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
                    // sh './jenkins/scripts/deliver.sh' 
                    deliver('./jenkins/scripts/deliver.sh')
                    input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                    // sh './jenkins/scripts/kill.sh'
                    terminate('./jenkins/scripts/kill.sh') 
                }
            }
        }
    }
}
