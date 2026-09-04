```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r backend/requirements.txt
                    pip install pytest
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest backend/tests
                '''
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                sh 'docker build -t k8s-backend:v1 ./backend'
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                sh 'docker build -t frontend:v1 ./frontend'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    kubectl apply -f backend/backend.yaml
                    kubectl apply -f frontend/frontend.yaml

                    kubectl rollout restart deployment/backend
                    kubectl rollout restart deployment/frontend

                    kubectl rollout status deployment/backend --timeout=120s
                    kubectl rollout status deployment/frontend --timeout=120s

                    kubectl get pods
                    kubectl get services
                '''
            }
        }
    }
}
```

