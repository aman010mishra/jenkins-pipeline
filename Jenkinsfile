pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nuclearcode070/simple-node-app'
    }

    
        
        stages {
                                      
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([credentialsId: 'b4839ef8-8fe1-4a91-9cf9-c792f251e7fe', url: '']) {
                    script {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }

        stage('Run App in Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name simple-node-app nuclearcode070/simple-node-app:latest'
            }
        }
        }
}
