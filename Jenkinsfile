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
    }

    post {
        success {
            echo 'Docker image created successfully!'
        }
    }
}
