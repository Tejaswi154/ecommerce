pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Build Frontend') {
            steps { sh 'cd frontend && npm install && npm run build' }
        }
        stage('Build Backend') {
            steps { sh 'cd backend && mvn clean package' }
        }
    }
}
