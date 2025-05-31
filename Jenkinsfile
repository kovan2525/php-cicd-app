pipeline {
    agent any

    environment {
        IMAGE_NAME = 'yourdockerhubusername/php-cicd-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/yourusername/php-cicd-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        docker.withRegistry('', 'dockerhub-creds') {
                            docker.image("${IMAGE_NAME}").push('latest')
                        }
                    }
                }
            }
        }
    }
}
