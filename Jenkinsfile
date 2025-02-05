pipeline {
    agent any

    environment {
        MINIKUBE_DOCKER_ENV = sh(script: "minikube docker-env", returnStdout: true).trim()
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/VincentNjoku/flask-ci-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'eval $(minikube docker-env) && docker build -t flask-app:latest .'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'docker run --rm flask-app pytest'
            }
        }

        stage('Deploy to Minikube') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
