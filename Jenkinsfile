pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "k8s-backend:v1"
        FRONTEND_IMAGE = "frontend:v1"
    }

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
                    export PYTHONPATH=$WORKSPACE
                    pytest backend/tests
                '''
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                sh '''
                    docker build -t $BACKEND_IMAGE ./backend
                '''
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                sh '''
                    docker build -t $FRONTEND_IMAGE ./frontend
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    kubectl apply -f k8s/
                    kubectl rollout status deployment/backend
                    kubectl rollout status deployment/frontend
                '''
            }
        }
    }
}
