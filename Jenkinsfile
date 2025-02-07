pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-static-site"
        CONTAINER_NAME = "my-static-container"
        PORT_MAPPING = "9000:80"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/krosri/Jenkins_Docker.git'  // Replace with your repo URL
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container
                    sh "docker stop ${CONTAINER_NAME} || true"
                    sh "docker rm ${CONTAINER_NAME} || true"

                    // Run new container
                    sh "docker run -d --name ${CONTAINER_NAME} -p ${PORT_MAPPING} ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        success {
            echo "Docker container running at http://localhost:9000"
        }
        failure {
            echo "Build or deployment failed!"
        }
    }
}
