pipeline {
    agent any
    tools {
        docker 'docker'  // Name of the Docker installation in Jenkins
    }

    environment {
        IMAGE_NAME = 'rental-car-booking'
        CONTAINER_NAME = 'rental-car-container'
        HOST_PORT = '8081'
        CONTAINER_PORT = '80'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                    docker run -d --name $CONTAINER_NAME -p $HOST_PORT:$CONTAINER_PORT $IMAGE_NAME
                '''
            }
        }
    }
}
