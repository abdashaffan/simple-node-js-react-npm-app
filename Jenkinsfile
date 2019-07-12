@Library('nodejs-library') _

pipeline {
    agent none
    environment { 
        CI = 'true'
    }
    stages {
        stage('check location') {
            agent {
                label 'build'
            }
            steps {
                sh 'pwd'
            }
        }
        stage('check version') {
            agent {
                label 'build'
            }
            steps {
                script {
                    version()
                }
            }
        }
        stage('Build') {
            agent {
                label 'build'
            }
            steps {
                script {
                    build()
                }
            }
        }
        stage('Test') {
            agent {
                label 'test'
            }
            steps {
                script {
                    test('./jenkins/scripts/test.sh')
                }
            }
        }
        stage('Deliver') {
            agent {
                label 'test'
            }
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
