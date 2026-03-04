pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/DharshanK24/Royal-CI-CD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t roadster-website .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop roadster-container || true
                docker rm roadster-container || true
                docker run -d -p 80:80 --name roadster-container roadster-website
                '''
            }
        }
    }
}