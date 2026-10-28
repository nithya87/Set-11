pipeline {
    agent any

    stages {
        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f "%WORKSPACE%\\k8s\\deployment.yaml"'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl rollout status deployment/set11-github-app --timeout=180s'
                bat 'kubectl get deployment set11-github-app'
                bat 'kubectl get pods -l app=set11-github-app'
            }
        }
    }
}