pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds') // Update if you used a different ID
        IMAGE_NAME = 'abhinay1206/spring-petclinic'  // Change to your Docker Hub repo
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Abhinay0208-Repobox/spring-petclinic.git'
            }
        }

        stage('Build App') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
