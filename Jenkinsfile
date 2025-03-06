pipeline {
    agent any
    stages {
        stage('Build') {
            steps { echo "Building the application..." }
        }
    }
    post {
        success {
            script {
                def recipient = credentials('EMAIL_RECIPIENTS')
                emailext subject: "✅ Jenkins Build Successful: ${JOB_NAME} #${BUILD_NUMBER}",
                         body: "The build for ${JOB_NAME} #${BUILD_NUMBER} was successful.\nCheck logs at ${BUILD_URL}",
                         to: recipient
            }
        }
        failure {
            script {
                def recipient = credentials('EMAIL_RECIPIENTS')
                emailext subject: "❌ Jenkins Build Failed: ${JOB_NAME} #${BUILD_NUMBER}",
                         body: "The build for ${JOB_NAME} #${BUILD_NUMBER} failed.\nCheck logs at ${BUILD_URL}",
                         to: recipient
            }
        }
    }
}
