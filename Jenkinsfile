pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'my-node-app'
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                git branch: 'nodejsApp', url: 'https://github.com/FezanMuhammadAli/practice-apps-for-cicd.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    // Here you can add any tests you want to run
                    // For now, we'll skip this step as it's a simple app
                    echo 'Running tests...'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    // Log in to Docker Hub (or AWS ECR if using ECR)
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                    // Push the image to Docker Hub (or AWS ECR)
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline successfully executed!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

