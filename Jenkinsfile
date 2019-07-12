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
                build()
            }
        }
        stage('Test') {
            steps {
                test('./jenkins/scripts/test.sh')
            }
        }
        stage('Deliver') { 
            steps {
                deliver('./jenkins/scripts/deliver.sh')
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                terminate('./jenkins/scripts/kill.sh') 
            }
        }
    }
}
