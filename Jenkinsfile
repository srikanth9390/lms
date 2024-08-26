pipeline {
    agent any
   }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'cd webapp && sudo docker container run --rm -e SONAR_HOST_URL="http://54.193.59.232:9000" -e SONAR_LOGIN="sqp_3018cc5eb3775eb8b7d4982ce65738fd56f075d0" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        stage('Release') {
            steps {
                echo 'Release Nexus'
                sh 'rm -rf *.zip'
                sh 'cd webapp && zip dist-lms1.1.zip -r dist'
                sh 'cd webapp && curl -v -u admin:Srikanth@9390 --upload-file dist-lms1.1.zip http://54.193.59.232/:8081/repository/lms/'
            }
        }
    }
}
