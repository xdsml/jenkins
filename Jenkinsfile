pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub'
        IMAGE_NAME = 'ismail402/monimagejenkins'
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {
        stage('Préparation') {
            steps {
                echo 'Début du pipeline Docker + SonarQube...'
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

       stage('Analyse SonarQube') {
    steps {
        withSonarQubeEnv('SonarLocal') {
            sh '''/opt/sonar-scanner/bin/sonar-scanner \
                -Dsonar.projectKey=tp-jenkins-sonar \
                -Dsonar.sources=. \
                -Dsonar.host.url=http://172.20.10.3:9000 \
                -Dsonar.login=$SONAR_TOKEN'''
        }
    }
}


    }
}
