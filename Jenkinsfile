pipeline{
    agent{
        label "vinod"
    }
    stages{
        stage("build"){
            steps{
                echo "========executing build========"
                sh "whoami"
                sh "docker build -t agency-app:1.0 ."
                echo "code build is completed"
            }
            }
        stage("docker push"){
            steps{
                echo "========executing docker push========"
                withCredentials([usernamePassword(credentialsId: 'dockerhub_cred',
                 usernameVariable: 'USERNAME',
                  passwordVariable: 'PASSWORD')]) {
                 
                sh "docker login -u ${env.USERNAME} -p ${env.PASSWORD}"
                sh "docker tag agency-app:1.0 ${env.USERNAME}/agency-app:1.0"
                sh "docker push ${env.USERNAME}/agency-app:1.0"
                echo "docker push is completed"
            }
            }
        }
        stage("test"){
            steps{
                echo "========executing test========"
            }
        }
        stage("deploy"){
            steps{
                echo "========executing deploy========"
                sh "docker run -d -p 80:80 --name agency-app agency-app:1.0"
            }
        }
    }
}

