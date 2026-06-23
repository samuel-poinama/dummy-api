pipeline {
    agent { label 'runner' }
    environment {
        IMAGE_NAME = 'samuelpoinama/dummy-api'
        VERSION = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/samuel-poinama/dummy-api.git'
            }
        }
        stage('Build') {
            steps {
                sh 'echo "build image"'
                sh 'docker build -t $IMAGE_NAME:$VERSION .'
            }
        }
        
        stage('Push') {
            steps {
                sh 'echo "push image"'
                sh 'docker push $IMAGE_NAME:$VERSION'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Lancement des tests..."'
                sh 'docker compose -f docker-compose.test.yaml up --build'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "deploy image"'
                sh 'docker compose -f docker-compose.yaml up -d'
            }
        }
    }
}