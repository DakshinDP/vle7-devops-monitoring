pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Load Image into Minikube') {
            steps {
                sh 'minikube image load myapp:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'kubectl rollout status deployment/myapp --timeout=120s'
                sh 'kubectl get pods -l app=myapp'
                sh 'kubectl get service myapp-service'
            }
        }
    }
}
