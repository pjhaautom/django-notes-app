pipeline{
    agent any
    stages{
        stage("clone code"){
            steps{
              echo "cloning from github" 
              git url:"https://github.com/pjhaautom/django-notes-app.git"
              
            }
            
            
        }
        stage("build"){
            steps{
                echo "building the code"
                sh "docker build -t newnoteapp2 ."
                
                
            }
        }
        stage("push to dockerhub"){
            steps{
                echo "pushing the image to dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubpass",usernameVariable:"dockerHubUser")]){
                sh "docker tag newnoteapp2 ${env.dockerhubUser}/newnoteapp2:latest "
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubpass}"
                sh "docker push ${env.dockerhubUser}/newnoteapp2:latest"
                }
                
            }
        }
        stage("deploy"){
            steps{
                echo "deploy the app"
                sh "docker-compose down && docker-compose up -d"
            
                
            }
        }
    }
    
    
    
}
