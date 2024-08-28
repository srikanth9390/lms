 pipeline {
    agent any

    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'dev', 'https://github.com/srikanth9390/lms.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("https://registry-1.docker.io/v2/nginx:latest
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry-1.docker.io/v2', 'dockerhub-credentials') {
                        dockerImage.push()
                    }
                }
            }
        }

       
    post {
        always {
            cleanWs()
        }
    }
}

