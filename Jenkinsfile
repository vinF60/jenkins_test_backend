pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/vinF60/jenkins_test_backend.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("backend-api:latest")
                }
            }
        }

        stage('Run Container') {
            steps {
                sh "docker rm -f backend || true"
                sh "docker run -d --name backend -p 3002:3002 backend-api:latest"
            }
        }
    }
}
