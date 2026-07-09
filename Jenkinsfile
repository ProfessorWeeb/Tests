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
                bat "\"C:\\Users\\Danie_000\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe\" build -t %IMAGE_NAME%:latest ."
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
                    echo %DOCKER_PASS% | "C:\\Users\\Danie_000\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" login -u %DOCKER_USER% --password-stdin
                    "C:\\Users\\Danie_000\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" push %IMAGE_NAME%:latest
                    "C:\\Users\\Danie_000\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" logout
                    """
                }
            }
        }
    }
}
