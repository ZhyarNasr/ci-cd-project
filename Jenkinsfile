pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t my-app .'
            }
        }
    }
}
