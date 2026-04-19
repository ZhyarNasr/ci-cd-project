pipeline {
    agent any

    environment {
        IMAGE_NAME = "zhyar1/php-app"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/ZhyarNasr/ci-cd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Corrected variable syntax
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    // Use double quotes to allow Jenkins to inject the credentials
                    sh "echo ${PASS} | docker login -u ${USER} --password-stdin"
                }
            }
        }

        stage('Push Image') {
            steps {
                sh "docker push ${IMAGE_NAME}:latest"
            }
        }
    }
}
