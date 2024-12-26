pipeline {
    agent any
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/asmajabr/node-todo-cicd.git", branch: "master"
                echo 'The Code got cloned'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t asmajaradat/demoimage ."
                echo 'Code has been built...'
            }
        }
        stage("scan image"){
            steps{
                echo 'image has been scanned'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker tag asmajaradat/demoimage asmajaradat/demoimage"
                sh "docker push asmajaradat/demoimage"
                echo 'image push done'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'deployment done'
            }
        }
    }
}
