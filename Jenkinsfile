pipeline {
    agent any

    environment {
        IMAGE_NAME = 'rental-car-booking'
        CONTAINER_NAME = 'rental-car-container'
        HOST_PORT = '8081'         // Jenkins UI uses 8080
        CONTAINER_PORT = '80'      // Change based on your app’s Dockerfile EXPOSE
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image: ${IMAGE_NAME}"
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    echo "Stopping and removing existing container if exists..."
                    sh "docker stop ${CONTAINER_NAME} || true"
                    sh "docker rm ${CONTAINER_NAME} || true"

                    echo "Running Docker container: ${CONTAINER_NAME}"
                    sh "docker run -d --name ${CONTAINER_NAME} -p ${HOST_PORT}:${CONTAINER_PORT} ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        success {
            echo "Deployment successful: http://localhost:${HOST_PORT}/"
        }
        failure {
            echo "Something went wrong during the pipeline!"
        }
    }
}
