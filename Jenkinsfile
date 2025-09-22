pipeline {
    agent any

    environment {
        JAVA_HOME = "/usr/lib/jvm/java-11-openjdk"
        PATH = "\/bin:\"
        NODE_HOME = "/usr/local/node"
        PATH = "\/bin:\"
    }

    tools {
        maven 'Maven 3.8.5'
        nodejs 'Node16'
        jdk 'Java11'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Tejaswi154/ecommerce.git'
            }
        }

        stage('Build React Frontend') {
            steps {
                dir('frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Build Spring Boot Backend') {
            steps {
                dir('backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Integrate Frontend & Backend') {
            steps {
                sh 'cp -r frontend/build/* backend/src/main/resources/static/'
            }
        }

        stage('Optional: Run Locally') {
            steps {
                dir('backend') {
                    sh 'java -jar target/backend-0.0.1-SNAPSHOT.jar &'
                }
            }
        }

        stage('Optional: Docker Deployment') {
            steps {
                sh '''
                docker build -t ecommerce-backend ./backend
                docker build -t ecommerce-frontend ./frontend
                docker network create ecommerce-net || true
                docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=ecommerce --network ecommerce-net mysql:8
                docker run -d --name backend --network ecommerce-net -p 8080:8080 ecommerce-backend
                docker run -d --name frontend -p 3000:3000 ecommerce-frontend
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}
