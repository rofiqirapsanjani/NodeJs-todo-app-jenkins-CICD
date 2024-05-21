pipeline {
    agent any
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/rofiqirapsanjani/NodeJs-todo-app-jenkins-CICD.git", branch: "master"
            }
        }
        stage("Build and Test"){
            steps{
                sh "bash build.sh"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub_id",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag node-app-test-new ${env.dockerHubUser}/node-app-test-new:${BUILD_NUMBER}"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/node-app-test-new:${BUILD_NUMBER}"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker run -p 8000:8000 -d sanjanivicky/node-app-test-new:${BUILD_NUMBER}"
            }
        }
    }
}
