pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'https://index.docker.io/v1'
        IMAGE_NAME = 'lms-app'
        VERSION = sh(script: "jq -r .version package.json", returnStdout: true).trim() // Adjust path if needed
    }

    stages {
        stage('Install jq') {
            steps {
                sh 'sudo apt-get update && sudo apt-get install -y jq' // Ensure jq is installed
            }
        }

        stage('Checkout Code') {
            steps {
                git 'https://github.com/srikanth9390/lms.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("https://index.docker.io/v1/ lms-app:latest")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        dockerImage.push()
                    }
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
