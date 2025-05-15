pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nuclearcode070/jenkins-pipeline'
        // IMAGE_NAME = 'aman010mishra/jenkins-pipeline'
        IMAGE_TAG = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/aman010mishra/jenkins-pipeline.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo Building the application...'
                // Add project build steps here
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh """
                            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                            docker push ${IMAGE_NAME}:${IMAGE_TAG}
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG} || true"
        }
    }
}

///hurray ab jake hua
