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
                        sh 'docker build -t $DOCKERHUB_USERNAME/mern-frontend:latest .'
                    }
                    // Build backend
                    dir('bezkoder-api') {
                        sh 'docker build -t $DOCKERHUB_USERNAME/mern-backend:latest .'
                    }
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                echo 'Pushing images to Docker Hub...'
                script {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh 'docker push $DOCKERHUB_USERNAME/mern-frontend:latest'
                    sh 'docker push $DOCKERHUB_USERNAME/mern-backend:latest'
                }
            }
        }
        
        stage('Cleanup') {
            steps {
                echo 'Logging out from Docker Hub...'
                sh 'docker logout'
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