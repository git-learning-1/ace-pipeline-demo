pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checked out from Git successfully!'
            }
        }

        stage('Parallel Checks') {
            parallel {
                stage('Validate BAR Structure') {
                    steps {
                        echo 'Validating ACE BAR file structure...'
                        sh 'sleep 3 && echo "BAR structure OK"'
                    }
                }
                stage('Unit Tests') {
                    steps {
                        echo 'Running unit tests on message flows...'
                        sh 'sleep 5 && echo "Unit tests passed"'
                    }
                }
                stage('Security Scan') {
                    steps {
                        echo 'Scanning for hardcoded credentials/vulnerabilities...'
                        sh 'sleep 4 && echo "Security scan clean"'
                    }
                }
            }
        }

        stage('Deploy to DEV') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'mq-creds', usernameVariable: 'MQ_USER', passwordVariable: 'MQ_PASS')]) {
                    echo "Deploying to DEV integration node as $MQ_USER"
                    sh 'echo "DEV deployment successful."'
                }
            }
        }

        stage('Deploy to TEST') {
            steps {
                echo 'Running integration tests on TEST environment...'
                sh 'echo "TEST deployment and validation successful."'
            }
        }

        stage('Approval Gate') {
            steps {
                input message: 'Deploy this build to PRODUCTION?', ok: 'Deploy'
            }
        }

        stage('Deploy to PROD') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'mq-creds', usernameVariable: 'MQ_USER', passwordVariable: 'MQ_PASS')]) {
                    echo "Deploying to PRODUCTION integration node as $MQ_USER"
                    sh 'echo "PROD deployment successful."'
                }
            }
        }
    }

    post {
        success {
            echo 'Full pipeline completed — DEV, TEST, and PROD all deployed.'
        }
        aborted {
            echo 'Pipeline was aborted — production was NOT touched.'
        }
    }
}
