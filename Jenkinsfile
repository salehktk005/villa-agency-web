pipeline{
    agent{
        label "vinod"
    }
    stages{
        stage("build"){
            steps{
                echo "========executing build========"
                sh "docker build -t agency-app:1.0 ."
                echo "code build is completed"
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
            }
        }
    }
}

