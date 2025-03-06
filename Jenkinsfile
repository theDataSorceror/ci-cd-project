pipeline {
    agent any
    environment {
        GREETING = "Hello, Jenkins!"
        DEPLOY_ENV = "staging"  // This can later be dynamically set (e.g., prod, dev)
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
                echo "Build Number: ${BUILD_NUMBER}"
                echo "Branch: ${GIT_BRANCH}"
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
                echo "Testing in environment: ${DEPLOY_ENV}"
            }
        }
        stage('Deploy') {
            steps {
                script {
                    if (DEPLOY_ENV == "staging") {
                        echo "Deploying to Staging..."
                    } else {
                        echo "Skipping Deployment"
                    }
                }
            }
        }
    }
}
