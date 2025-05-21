pipeline {
    agent any

    tools {
        maven 'Maven 3.9.6' // This must match the name you configured in Jenkins
    }

    environment {
        TOMCAT_URL = 'http://<Tomcat-Server-IP>:8080/manager/text'
        TOMCAT_CREDENTIALS = 'tomcat-credentials-id' // Set this up in Jenkins > Credentials
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/yaswanth70/Hello-world.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: "${TOMCAT_CREDENTIALS}", 
                                          path: '', 
                                          url: "${TOMCAT_URL}")], 
                       war: '**/target/*.war'
            }
        }
    }

    post {
        success {
            echo "Deployment successful!"
        }
        failure {
            echo "Something went wrong!"
        }
    }
}
