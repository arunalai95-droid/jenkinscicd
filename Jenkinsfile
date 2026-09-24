pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/arunalai95-droid/jenkinscicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-devops-website:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                    docker stop mywebsite || true
                    docker rm mywebsite || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                    docker run -d \
                    --name mywebsite \
                    -p 80:8080 \
                    my-devops-website:latest
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
