pipeline {
    agent any

    environment {
        // Your Docker Hub repository name
        IMAGE_NAME = "san1123/php-app"
    }

    stages {
        // Stage 1: Jenkins does a 'Declarative Checkout' automatically, 
        // but this manual stage ensures your files are in the right place.
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/ZhyarNasr/ci-cd-project.git'
            }
        }

        // Stage 2: Building the image using Windows Batch (bat)
        stage('Build Docker Image') {
            steps {
                // In Windows 'bat' blocks, we use %VARIABLE_NAME%
                bat "docker build -t %IMAGE_NAME%:latest ."
            }
        }

        // Stage 3: Authenticating with Docker Hub
        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds', 
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    // Windows echo handles the password pipe slightly differently than Linux
                    bat "echo %PASS% | docker login -u %USER% --password-stdin"
                }
            }
        }

        // Stage 4: Pushing the final image
        stage('Push Image') {
            steps {
                bat "docker push %IMAGE_NAME%:latest"
            }
        }
    }
}
