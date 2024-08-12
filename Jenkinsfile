pipeline {
    agent any 
    
    stages {
        stage("Clone Code") {
            steps {
                echo "Cloning the code"
                git url: "https://github.com/vipulwarthe/django-notes-app.git", branch: "main"
            }
        }
        stage("Build") {
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Tag and Push to Docker Hub") {
            steps {
                echo "Tagging and pushing the image to Docker Hub"
                withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {
                    // Tagging the image with 'latestnew' tag
                    sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latestnew"
                    // Logging into Docker Hub
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    // Pushing the image with 'latestnew' tag
                    sh "docker push ${env.dockerHubUser}/my-note-app:latestnew"
                }
            }
        }
        stage('Install Docker Compose and Deploy') {
            steps {
                sh 'curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o $HOME/docker-compose'
                sh 'chmod +x $HOME/docker-compose'
                sh '$HOME/docker-compose --version'
                sh 'export PATH=$PATH:$HOME && $HOME/docker-compose down && $HOME/docker-compose up -d'
            }
        }
    }
}


