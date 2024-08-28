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
                    // Read version from package.json
                    def version = sh(returnStdout: true, script: 'cat package.json | jq -r .version').trim()

                    // Build image with version tag
                    docker.build "lms:version"
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

