pipeline {
    agent any

    tools {
        maven 'Maven3'   // Make sure Maven is configured in Jenkins
        jdk 'JDK17'      // Make sure JDK is configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/abhijitnalawade0101/jenkins-ci-cd-pipeline.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Copy WAR to Docker context') {
            steps {
                sh 'cp target/*.war ./Docker/MyWebApp.war'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                cd Docker
                sudo docker build -t mywebapp:v1 .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                sudo docker stop registerapp || true
                sudo docker rm registerapp || true
                sudo docker run -d --name registerapp -p 8086:8080 mywebapp:v1
                '''
            }
        }
    }
}

