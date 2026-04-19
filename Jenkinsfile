pipeline {
    agent any

    tools {
        // This MUST match the 'Name' you gave in Global Tool Configuration
        dockerTool 'Docker'
    }

    environment {
        IMAGE_NAME = "zhyar1/php-app"
    }

    stages {
        stage('Clone Repo') {
            steps {
                // Ensure this matches your repository
                git branch: 'main', url: 'https://github.com/ZhyarNasr/ci-cd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Using ${} for Linux/Jenkins environment variables
                bat "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds', // Ensure this ID exists in Jenkins Credentials
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    // Logs in using the credentials defined in Jenkins
                    bat "echo ${PASS} | docker login -u ${USER} --password-stdin"
                }
            }
        }

        stage('Push Image') {
            steps {
                bat "docker push ${IMAGE_NAME}:latest"
            }
        }
    }
}
