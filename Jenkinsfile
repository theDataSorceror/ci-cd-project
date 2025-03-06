pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Building the application..."
            }
        }
    }
    post {
        success {
            script {
                withCredentials([string(credentialsId: 'EMAIL_RECIPIENTS', variable: 'EMAIL')]) {
                    echo "📧 DEBUG: Email recipient is: ${EMAIL}"  // This will print the email to console logs
                    emailext subject: "✅ Jenkins Build Successful: ${JOB_NAME} #${BUILD_NUMBER}",
                             body: "The build for ${JOB_NAME} #${BUILD_NUMBER} was successful.\nCheck logs at ${BUILD_URL}",
                             to: "${EMAIL}",
                             replyTo: "${EMAIL}",
                             debug: true // Enables email sending debug logs
                }
            }
        }
        failure {
            script {
                withCredentials([string(credentialsId: 'EMAIL_RECIPIENTS', variable: 'EMAIL')]) {
                    echo "📧 DEBUG: Email recipient is: ${EMAIL}"  // Debugging step for failure
                    emailext subject: "❌ Jenkins Build Failed: ${JOB_NAME} #${BUILD_NUMBER}",
                             body: "The build for ${JOB_NAME} #${BUILD_NUMBER} failed.\nCheck logs at ${BUILD_URL}",
                             to: "${EMAIL}",
                             replyTo: "${EMAIL}",
                             debug: true // Enables email sending debug logs
                }
            }
        }
    }
}
