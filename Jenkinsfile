pipeline {
    agent any

    stages {
        stage('Setup Minikube Docker') {
            steps {
                sh 'sudo chmod +x /usr/local/bin/minikube'
                sh 'sudo usermod -aG docker $USER'
                sh 'eval $(minikube docker-env)'
            }
        }

        stage('Build Docker Image') {
            steps {
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
