pipeline {
    agent any
    
    stages{
        stage("cloning"){
            steps{
                echo "cloning git"
                git url: "https://github.com/hashmi77/django-notes-app.git", branch: "main"
            }
            
        }
        stage("build"){
            steps{
                echo "build code" 
                sh "docker build -t mynote ."
            }
        }
        stage("push imgaes"){
            steps{
                echo "pushimages on hub"
                withCredentials([usernamePassword(credentialsId: "hashmi",passwordVariable:"hashmipass",usernameVariable:"hashmiUser")]){
                sh "docker tag mynote ${env.hashmiUser}/mynote:latest"
                sh "docker login -u ${env.hashmiUser} -p ${env.hashmipass}"
                sh "docker push ${env.hashmiUser}/mynote:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                echo "deploy"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }

}
