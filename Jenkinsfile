pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/lalmon149/django-notes-app.git", branch: "main"
            }
            
        }
        stage("build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-notes-app ."
                
            }
            
        }
        stage("push to docker Hub"){
            steps {
                echo "Pushing the image to docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-notes-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deplyoing the container"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
