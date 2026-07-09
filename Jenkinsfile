pipeline {
    agent any

    environment {
        IMAGE_NAME = 'professorweeb/test'
        DOCKER_EXE = 'C:\\Users\\Danie_000\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
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
                bat "\"%DOCKER_EXE%\" build -t %IMAGE_NAME%:latest ."
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
                    echo %DOCKER_PASS% | "%DOCKER_EXE%" login -u %DOCKER_USER% --password-stdin
                    "%DOCKER_EXE%" push %IMAGE_NAME%:latest
                    "%DOCKER_EXE%" logout
                    """
                }
            }
        }
    }
}
    }
}
