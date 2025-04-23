
pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('rental-car-booking')
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image('rental-car-booking').run('-d -p 8080:80')
                }
            }
        }
    }
}
