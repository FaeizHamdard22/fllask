pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-jenkins-gitapp"
        CONTAINER_NAME = "flask-jenkins-container"
        PORT = "83"
    }

    stages {
        stage('Checkout from GitHub') {
            steps {
                git branch: 'main',
                    url: 'git@github.com:FaeizHamdard22/fllask.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "🔨 Building image ${IMAGE_NAME}"
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Container') {
            steps {
                echo "🚀 Running container ${CONTAINER_NAME}"
                sh """
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d --name ${CONTAINER_NAME} -p ${PORT}:5000 ${IMAGE_NAME}
                """
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Access via http://localhost:${PORT}"
        }
        failure {
            echo "❌ Deployment failed. Check the logs."
        }
    }
}

