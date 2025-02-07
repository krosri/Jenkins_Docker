pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-docker-app"
        CONTAINER_NAME = "jenkins-docker-container"
        PORT_MAPPING = "9000:80"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/krosri/Jenkins_Docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "sudo docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container
                    sh "sudo docker stop ${CONTAINER_NAME} || true"
                    sh "sudo docker rm ${CONTAINER_NAME} || true"

                    // Run new container
                    sh "sudo docker run -d --name ${CONTAINER_NAME} -p ${PORT_MAPPING} ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        success {
            echo "Docker container is running at http://localhost:9000"
        }
        failure {
            echo "Build or deployment failed!"
        }
    }
}
