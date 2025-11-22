pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        DOCKERHUB_USERNAME = 'sreehitha23'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }
        
        stage('Build Docker Images') {
            steps {
                echo 'Building Docker images...'
                script {
                    // Build frontend
                    dir('bezkoder-ui') {
                        bat 'docker build -t %DOCKERHUB_USERNAME%/mern-frontend:latest .'
                    }
                    // Build backend
                    dir('bezkoder-api') {
                        bat 'docker build -t %DOCKERHUB_USERNAME%/mern-backend:latest .'
                    }
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                echo 'Pushing images to Docker Hub...'
                script {
                    bat 'echo %DOCKERHUB_CREDENTIALS_PSW% | docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin'
                    bat 'docker push %DOCKERHUB_USERNAME%/mern-frontend:latest'
                    bat 'docker push %DOCKERHUB_USERNAME%/mern-backend:latest'
                }
            }
        }
        
        stage('Cleanup') {
            steps {
                echo 'Logging out from Docker Hub...'
                bat 'docker logout'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}