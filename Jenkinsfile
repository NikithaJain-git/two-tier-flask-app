pipeline {
    agent any;
    stages {
        stage ("code") {
            steps {
                git url: "https://github.com/NikithaJain-git/two-tier-flask-app.git", branch: "master"
                }
        }
        stage ("Build") {
            steps {
                sh "docker build -t trainwithshubham/two-tier-flask-app ."
            }
        }
        stage ("Docker push") {
            steps {withCredentials ([usernamePassword(credentialsId:"dockerhubuser",
            usernameVariable:"dockerhubuser",
            passwordVariable:"dockerhubpass"
            )]){
                sh "docker image tag trainwithshubham/two-tier-flask-app:latest ${env.dockerhubuser}/two-tier-flask-app:latest"
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                sh "docker push ${env.dockerhubuser}/two-tier-flask-app:latest"
            }
            }
        }
        stage ("Deploy") {
            steps {
                sh "docker compose up -d"
            }
        }
    }
}

