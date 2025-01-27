pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'engcountio/my-node-app' // Change to your Docker Hub username
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'nodejsApp', url: 'https://github.com/FezanMuhammadAli/practice-apps-for-cicd.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    echo 'Running tests...'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "DOCKER_CREDENTIALS", passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                        sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                        sh 'docker push $DOCKER_IMAGE'
                    }
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
