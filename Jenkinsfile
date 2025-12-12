pipeline {
    agent any

    environment {
        IMAGE = "salehktk16/agency_wala"
        CONTAINER = "agency_wala_container"
        PORT = "8080"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/salehktk005/villa-agency-web.git'
            }
        }

        stage('Test Website') {
            steps {
                echo "Running basic website tests..."
                sh '''
                    if [ -f index.html ]; then
                        echo "✔ index.html found"
                    else
                        echo "❌ index.html missing"
                        exit 1
                    fi
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh "docker build -t ${IMAGE}:latest ."
            }
        }

        stage('Deploy Container') {
            steps {
                echo "Deploying container..."
                sh """
                    docker stop ${CONTAINER} || true
                    docker rm ${CONTAINER} || true
                    docker run -d -p ${PORT}:80 --name ${CONTAINER} ${IMAGE}:latest
                """
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Visit http://localhost:${PORT}"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
