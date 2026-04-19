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
                sh "docker build -t %IMAGE_NAME%:latest ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh """
                    echo %PASS% | docker login -u %USER% --password-stdin
                    """
                }
            }
        }

        stage('Push Image') {
            steps {
                sh "docker push %IMAGE_NAME%:latest"
            }
        }
    }
}
