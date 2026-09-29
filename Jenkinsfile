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
                        sh 'sleep 3 && echo "BAR structure OK"'
                    }
                }
                stage('Unit Tests') {
                    steps {
                        sh 'sleep 5 && echo "Unit tests passed"'
                    }
                }
                stage('Security Scan') {
                    steps {
                        // Intentionally fail this one to test failure handling
                        sh 'sleep 2 && echo "Vulnerability found!" && exit 1'
                    }
                }
            }
        }

        stage('Deploy to DEV') {
            steps {
                echo 'Deploying to DEV integration node...'
                sh 'echo "DEV deployment successful."'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully.'
        }
        failure {
            echo '❌ Pipeline FAILED — likely cause: security scan or validation error.'
            echo 'In a real setup, this is where Slack/email notifications would fire.'
        }
        always {
            echo 'Cleanup step: removing temporary BAR files, closing connections, etc.'
        }
    }
}
