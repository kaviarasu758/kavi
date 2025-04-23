pipeline {
    agent any

    environment {
        IMAGE_NAME = 'rental-car-booking'
        CONTAINER_NAME = 'rental-car-container'
        HOST_PORT = '8081'  // Jenkins uses 8080, so we changed this to 8081
        CONTAINER_PORT = '80'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any previous containers with the same name
                    sh 'docker stop $CONTAINER_NAME || true'
                    sh 'docker rm $CONTAINER_NAME || true'
                    // Run the container
                    sh 'docker run -d --name $CONTAINER_NAME -p $HOST_PORT:$CONTAINER_PORT $IMAGE_NAME'
                }
            }
        }
    }
}
