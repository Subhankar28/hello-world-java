pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'docker-hub-credentials'  // Jenkins credentials ID for Docker Hub login
        IMAGE_NAME = 'hello-world-java'
        DOCKER_REGISTRY = 'docker.io'
        TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout from the default branch (replace 'main' with your branch if needed)
                    checkout scm
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t ${DOCKER_REGISTRY}/${IMAGE_NAME}:${TAG} .'
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using Jenkins credentials
                    docker.withRegistry('', DOCKER_HUB_CREDENTIALS) {
                        echo 'Logged in to Docker Hub'
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the image to Docker Hub
                    sh 'docker push ${DOCKER_REGISTRY}/${IMAGE_NAME}:${TAG}'
                }
            }
        }
    }

    post {
        always {
            // Clean up any resources after the pipeline completes
            cleanWs()
        }
    }
}
