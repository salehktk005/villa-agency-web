pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/salehktk005/villa-agency-web.git'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh ''' 
                    if [ -f package.json ]; then
                        npm install
                        npm test || true
                    else
                        echo "No tests found."
                    fi
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh """
                    docker build -t salehktk16/agency_wala:latest .
                """
            }
        }

        stage('Run Container') {
            steps {
                echo "Running container..."
                sh """
                    docker stop agency_wala_container || true
                    docker rm agency_wala_container || true
                    docker run -d -p 8080:80 --name agency_wala_container salehktk16/agency_wala:latest
                """
            }
        }

        // OPTIONAL — only add if you want to push image to Docker Hub
        /*
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh """
                        echo "$PASS" | docker login -u "$USER" --password-stdin
                        docker push salehktk16/agency_wala:latest
                    """
                }
            }
        }
        */
    }
}
