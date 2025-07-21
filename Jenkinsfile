pipeline {
    agent any

    environment {
        IMAGE_NAME = "abhinay1206/spring-petclinic"  // Change to your Docker Hub repo
    }
    stages {
        stage('Checkout') {
            steps {
                
                git branch: 'main', url: 'https://github.com/Abhinay0208-Repobox/spring-petclinic.git'
            }
        }

        stage('Build Jar') {
            steps {
                 sh 'mvn clean install -DskipTests -Dmaven.compiler.release=17'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh """
                        echo "$PASSWORD" | docker login -u "$USERNAME" --password-stdin
                        docker push $IMAGE_NAME
                    """
                }
            }
        }
    }
}

