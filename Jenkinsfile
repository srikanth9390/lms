pipeline {
    agent any

    stages {
        // Stage 1: Checkout Code
        stage('Checkout Code') {
            steps {
                git branch: 'dev', url: 'https://github.com/srikanth9390/lms.git'
            }
        }

        // Stage 2: Build Docker Image
        stage('Build Docker Image') {
            steps {
                script {
                    // Read version from package.json
                    def version = sh(returnStdout: true, script: 'cat package.json | jq -r .version').trim()

                    // Build image with version tag
                    docker.build "lms:latest"
                }
            }
        }

        // Stage 3: Push Docker Image (requires credentials)
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'https://index.docker.io/v1', usernameVariable:   
 'srikanth1322', passwordVariable: 'Srikanth@9390')]) {
                    sh "docker login -u srikanth1322 -p Srikanth@9390 https://index.docker.io/v1"
                    sh "docker push lms:latest"
                }
            }
        }
