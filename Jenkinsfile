pipeline {
    agent any  // Runs on any available Jenkins agent

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/VincentNjoku/flask-ci-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'eval $(minikube docker-env)'  // Use Minikube’s local Docker registry
                sh 'docker build -t flask-app:latest .'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'docker run --rm flask-app pytest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
