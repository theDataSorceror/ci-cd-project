pipeline {
    agent any

    stages {
            stage('Build') {
            steps {
                echo "Building the application..."
                sh 'echo "This is a build artifact" > artifact.txt'  // Example file
                archiveArtifacts artifacts: 'artifact.txt', fingerprint: true
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'echo "<testsuite><testcase classname=\\"ExampleTest\\" name=\\"Test1\\"/></testsuite>" > test-results.xml'
                junit 'test-results.xml'
            }
        }
    }

    post {
        success {
            script {
                // Using withCredentials to securely fetch the email
                withCredentials([string(credentialsId: 'EMAIL_RECIPIENTS', variable: 'EMAIL')]) {
                    echo "📧 DEBUG: Email recipient is: ${EMAIL}"  // Debugging step
                    emailext subject: "✅ Jenkins Build Successful: ${JOB_NAME} #${BUILD_NUMBER}",
                             body: "The build for ${JOB_NAME} #${BUILD_NUMBER} was successful.\nCheck logs at ${BUILD_URL}",
                             to: "${EMAIL}",
                             replyTo: "${EMAIL}"  // Using the email from the credentials
                }
            }
        }
        failure {
            script {
                // Using withCredentials to securely fetch the email
                withCredentials([string(credentialsId: 'EMAIL_RECIPIENTS', variable: 'EMAIL')]) {
                    echo "📧 DEBUG: Email recipient is: ${EMAIL}"  // Debugging step
                    emailext subject: "❌ Jenkins Build Failed: ${JOB_NAME} #${BUILD_NUMBER}",
                             body: "The build for ${JOB_NAME} #${BUILD_NUMBER} failed.\nCheck logs at ${BUILD_URL}",
                             to: "${EMAIL}",
                             replyTo: "${EMAIL}"  // Using the email from the credentials
                }
            }
        }
    }
}
