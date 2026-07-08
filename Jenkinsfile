pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t employee-portal:latest .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh 'docker stop employee-portal || true'
                sh 'docker rm employee-portal || true'
                sh 'docker run -d --name employee-portal -p 8082:80 employee-portal:latest'
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }
    }
}
