pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Bhushanrajput/devops-practice-project-Bh.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devops-website .'
            }
        }

    }
}