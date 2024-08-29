pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'https://index.docker.io/v1/'
        IMAGE_NAME = 'lms-app'
        VERSION = sh(script: "jq -r .version webapp/package.json", returnStdout: true).trim()
        IMAGE_TAG = "https://index.docker.io/v1/lms-app:latest"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'dev', url: 'https://github.com/srikanth9390/lms.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                     sh "sudo docker build -t srikanth1322/lms-app:latest -f webapp/Dockerfile ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'srikanth1322', usernameVariable: 'srikanth1322', passwordVariable: 'Srikanth@9390')]) {
                       sh "echo Srikanth@9390 | sudo docker login -u srikanth1322 --password-stdin"
                       sh "sudo docker push srikanth1322/lms-app:latest"
                    }
                }
            }
        }
    }
}

                      

                


   
