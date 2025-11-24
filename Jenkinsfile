pipeline {
    agent any

    environment {
        DOCKERHUB_USER = credentials('dockerhub-user')
        DOCKERHUB_PASS = credentials('dockerhub-pass')
    }

    stages {
        stage('Checkout') {
            steps { git 'https://github.com/YOUR/BackendRepo.git' }
        }

        stage('Build Docker Image') {
            steps { sh 'docker build -t youruser/backend:latest .' }
        }

        stage('Login to DockerHub') {
            steps { sh 'echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin' }
        }

        stage('Push Image') {
            steps { sh 'docker push youruser/backend:latest' }
        }

        stage('Deploy') {
            steps { sh 'docker compose -f /opt/deploy/docker-compose.yml pull && docker compose -f /opt/deploy/docker-compose.yml up -d' }
        }
    }
}
