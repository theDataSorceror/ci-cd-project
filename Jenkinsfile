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
                withCredentials([string(credentialsId: 'EMAIL_RECIPIENTS', variable: 'EMAIL')]) {
                    emailext subject: "✅ Jenkins Build Successful: ${JOB_NAME} #${BUILD_NUMBER}",
                             body: "The build for ${JOB_NAME} #${BUILD_NUMBER} was successful.\nCheck logs at ${BUILD_URL}",
                             to: EMAIL,
                             replyTo: "thedatasorceror@archtrace.io"
                }
            }
        }
        failure {
            script {
                withCredentials([string(credentialsId: 'EMAIL_RECIPIENTS', variable: 'EMAIL')]) {
                    emailext subject: "❌ Jenkins Build Failed: ${JOB_NAME} #${BUILD_NUMBER}",
                             body: "The build for ${JOB_NAME} #${BUILD_NUMBER} failed.\nCheck logs at ${BUILD_URL}",
                             to: EMAIL,
                             replyTo: "thedatasorceror@archtrace.io"
                }
            }
        }
    }
}
