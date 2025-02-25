pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "nkay8/myapp:latest"
    }

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $DOCKER_IMAGE ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'docker-hub-password', variable: 'DOCKER_PASSWORD')]) {
                    sh "echo $DOCKER_PASSWORD | docker login -u nkay8 --password-stdin"
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh "docker push $DOCKER_IMAGE"
            }
        }
    }
}
