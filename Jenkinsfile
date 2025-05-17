pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub' // ID du credential Jenkins
        IMAGE_NAME = 'ismail402/monimagejenkins' // Ton vrai nom d’image DockerHub
    }

    stages {
        stage('Préparation') {
            steps {
                echo 'Début du pipeline Docker...'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
    }
}
