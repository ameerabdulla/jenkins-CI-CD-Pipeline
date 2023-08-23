pipeline {
    agent any
    
    stages {
        stage("code"){
            steps {
                echo "this is code"
                git url:"https://github.com/ameerabdulla/jenkins-CI-CD-Pipeline.git", branch:"main"
            }
        }
        stage("build"){
            steps {
                echo "this is build"
                sh "docker build -t image1 ."
            }
        }
        stage("push"){
            steps {
                echo "this is push"
                withCredentials([usernamePassword(credentialsId:"ameerabdulla42",passwordVariable:"password", usernameVariable:"username")]) {
                sh "docker login -u ${env.username} -p ${env.password}"
                sh "docker tag image1 ${env.username}/image1:lastest1"
                sh "docker push ${env.username}/image1:lastest1"
                }
            }
        }
        stage("deploy"){
            steps {
                echo "this is deploy"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
