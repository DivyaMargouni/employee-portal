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
                 sh 'minikube image load employee-portal:latest'
            }
        }
       stage('Deploy to Kubernetes') {
    steps {
        sh 'eval $(minikube docker-env) && docker build -t employee-portal:latest .'
        sh 'kubectl apply -f k8s/deployment.yaml'
        sh 'kubectl apply -f k8s/service.yaml'
        sh 'kubectl rollout restart deployment employee-portal'
        sh 'kubectl get pods'
    }
}

    
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }
    }
}
