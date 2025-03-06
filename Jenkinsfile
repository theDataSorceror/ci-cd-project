pipeline {
    agent any
    environment {
        RECIPIENTS = "${env.EMAIL_RECIPIENTS}"
    }
    stages {
        stage('Clone Repo') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo "Building the application..."
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying application..."
            }
        }
    }
    post {
        success {
            emailext subject: "✅ Jenkins Build Successful: ${JOB_NAME} #${BUILD_NUMBER}",
                     body: "Great job! The build for ${JOB_NAME} #${BUILD_NUMBER} was successful.\nCheck logs at ${BUILD_URL}",
                     to: "${RECIPIENTS}"
        }
        failure {
            emailext subject: "❌ Jenkins Build Failed: ${JOB_NAME} #${BUILD_NUMBER}",
                     body: "Oops! The build for ${JOB_NAME} #${BUILD_NUMBER} failed.\nCheck logs at ${BUILD_URL}",
                     to: "${RECIPIENTS}"
        }
    }
}
