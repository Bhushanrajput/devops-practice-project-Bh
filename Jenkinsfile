pipeline {
    agent any

    environment {
        IMAGE_NAME = "bhushan432/devops-website"
        CONTAINER_NAME = "devops-container"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Bhushanrajput/devops-practice-project-Bh.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %IMAGE_NAME%'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker stop %CONTAINER_NAME% || exit 0'
            }
        }

        stage('Remove Old Container') {
            steps {
                bat 'docker rm %CONTAINER_NAME% || exit 0'
            }
        }

        stage('Run New Container') {
            steps {
                bat 'docker run -d -p 8081:80 --name %CONTAINER_NAME% %IMAGE_NAME%'
            }
        }

    }
}