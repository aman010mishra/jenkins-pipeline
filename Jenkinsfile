pipeline {
    agent any

    environment {
        IMAGE_NAME = 'yourdockerhubusername/simple-node-app'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/aman010mishra/jenkins-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                    script {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }

        stage('Run App in Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name simple-node-app yourdockerhubusername/simple-node-app:latest'
            }
        }
    }
}
