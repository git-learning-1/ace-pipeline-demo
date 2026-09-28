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
                sh '''
                    echo "Validating ACE BAR file structure..."
                    echo "app_name=OrderProcessingFlow" > bar_metadata.txt
                    cat bar_metadata.txt
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo "Deployment to integration node: SUCCESS"'
            }
        }
    }
}
// TEST Change
