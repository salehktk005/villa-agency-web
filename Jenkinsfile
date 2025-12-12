pipeline {
    agent any

    environment {
        IMAGE_NAME = "salehktk16/agency_wala"
        TAG = "latest"
    }

    stages {    

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove old container if exists
                    sh "docker rm -f agency_wala_container || true"
                    // Run new container
                    sh "docker run -d -p 80:80 --name agency_wala_container ${IMAGE_NAME}:${TAG}"
                }
            }
        }
    }

    post {
        success {
            echo "✅ Dockerized website is up and running at http://localhost"
        }
        failure {
            echo "❌ Deployment failed"
        }
    }
}
