pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checked out from Git successfully!'
            }
        }
        stage('Validate BAR') {
            steps {
                sh 'echo "Validating ACE BAR file structure..."'
            }
        }
        stage('Deploy with MQ credentials') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'mq-creds', usernameVariable: 'MQ_USER', passwordVariable: 'MQ_PASS')]) {
                    sh 'echo "Connecting to MQ as user: $MQ_USER"'
                    sh 'echo "Password length check: ${#MQ_PASS} characters"'
                }
            }
        }
    }
}
