pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/KundanSingh08/chatbot-deployment.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('chatbot:latest')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        docker.image('chatbot:latest').push('latest')
                    }
                }
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 chatbot:latest'
            }
        }
    }
}
