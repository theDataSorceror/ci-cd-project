pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                checkout scm  // This automatically uses GitHub repository and branch configured in Jenkins
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
