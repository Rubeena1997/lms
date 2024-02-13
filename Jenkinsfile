pipeline {
    agent any

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
                sh 'cd webapp && docker run --rm -e SONAR_HOST_URL="http://54.175.148.193:9000" -e SONAR_LOGIN="squ_c05edfd52ca9d180bac6aa82d2c4d2f87aaf17a4" -v "$(pwd):/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'

            }
        }
        stage('Release') {
            steps {
                echo 'Release Nexus'
                sh 'rm -rf *.zip'
                sh 'cd webapp && zip dist-lms.zip -r dist'
                sh 'cd webapp && curl -v -u admin:Rubeena --upload-file dist-lms.zip http://54.175.148.193:8081/repository/lms/'
            }
        }
    }
}
