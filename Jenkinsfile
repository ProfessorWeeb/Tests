pipeline {
    agent any

    environment {
        IMAGE_NAME = 'professorweeb/test'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/professorweeb/Tests.git'
            }
        }

        stage('Build Docker image') {
            steps {
                bat "\"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe\" build -t %IMAGE_NAME%:latest ."
            }
        }

        stage('Push to Dockerhub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'docker',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    bat """
                    echo %DOCKER_PASS% |
                    "C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" login -u %DOCKER_USER% --password-stdin
                    
                    "C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" push %IMAGE_NAME%:latest
                    
                    "C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" logout
                    """
                }
            }
        }
    }
}
