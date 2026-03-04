pipeline {
    agent any

    environment {
        IMAGE_NAME = "roadster-website"
        CONTAINER_NAME = "roadster-container"
        HOST_PORT = "8090"    // change if needed
        CONTAINER_PORT = "80"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/DharshanK24/Royal-CI-CD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh """
                    docker build -t ${IMAGE_NAME}:latest .
                    """
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh """
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                    """
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    sh """
                    docker run -d \
                    -p ${HOST_PORT}:${CONTAINER_PORT} \
                    --name ${CONTAINER_NAME} \
                    ${IMAGE_NAME}:latest
                    """
                }
            }
        }

        stage('Cleanup Dangling Images') {
            steps {
                sh 'docker image prune -f'
            }
        }
    }

    post {
        success {
            echo "✅ Deployment Successful!"
        }
        failure {
            echo "❌ Pipeline Failed!"
        }
    }
}