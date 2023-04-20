pipeline {
    agent any
    
    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/saranya-d/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build and Test'){
            steps {
                poweshell 'docker build . -t saranyadittakavi/webapp:v1' 
            }
        }
        stage('Login and Push Image'){
            steps {
                echo 'logging in to docker hub and pushing image..'
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUser')]) {
                    powershell "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    powershell "docker push saranyadittakavi/webapp:v1"
                }
            }
        }
        stage('Deploy'){
            steps {
                poweshell 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
