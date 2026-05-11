pipeline {
    agent any

    environment {
        IMAGE_NAME = "bhushan432/devops-website"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/Bhushanrajput/devops-practice-project-Bh.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat 'docker push %IMAGE_NAME%:latest'
                }
            }
        }

    }
}