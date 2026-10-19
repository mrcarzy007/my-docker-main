pipeline {
    agent any
    
    environment {
        DOCKER_HUB_USER = "devopsaditya123"
        IMAGE_NAME = "${DOCKER_HUB_USER}/app"
        IMAGE_TAG = "v1.0.${BUILD_NUMBER}"
    }
    
    stages {
        stage('1. Checkout') {
            steps {
                echo "Github code successfully checkout!"
            }
        }
        
        stage('2. Build Docker Image') {
            steps {
                echo "Building image: ${env.IMAGE_NAME}:${env.IMAGE_TAG}"
                sh "docker build -t ${env.IMAGE_NAME}:${env.IMAGE_TAG} ."
            }
        }
        
        stage('3. Push to Docker Hub') {
            steps {
                echo "Pushing to Docker Hub..."
                withCredentials([usernamePassword(credentialsId: 'docker-hub-pass', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh "docker push ${env.IMAGE_NAME}:${env.IMAGE_TAG}"
                }
            }
        }
    }
}