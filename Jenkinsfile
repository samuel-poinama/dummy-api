pipeline {
    agent { label 'runner' }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/samuel-poinama/dummy-api.git'
            }
        }
        stage('Build') {
            steps {
                sh 'echo "build image"'
                sh 'docker compose build'
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