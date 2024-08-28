pipeline {
    agent any

    stages {
        stage("Clone Code") {
            steps {
                echo "Cloning the code"
                git url: "https://github.com/KevDen01/kevin_app.git", branch: "main"
            }
        }

        stage("Build") {
            steps {
                echo "Building the Docker image"
                sh "sudo docker build -t kevin_app ."
            }
        }

        stage("Push to Docker Hub") {
            steps {
                echo "Pushing image to Docker Hub"
                withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: "Salamandra-92", usernameVariable: "kevinklein01")]) {
                    sh "sudo docker tag test-app ${env.dockerHubUser}/kevin_app:latest"
                    sh "sudo docker login -u -S ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "sudo docker push ${env.dockerHubUser}/kevin_app:latest"
                }
            }
        }

        stage ("Deploy") {
            steps {
                echo "Deploying the container"
                sh "sudo docker compose down && docker compose up -d"
            }
        }
    }
}
