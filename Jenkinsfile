pipeline {
    agent {label ''}
    stages {
        stage("code") {
            steps {
                git url: "https://github.com/Pratul99/node-todo-cicd.git", branch: "main"
            }
        }
        stage("build & test") {
            steps {
                sh "docker build . -t pratulb/node-app"
            }
        }
        stage("Pushing to repo") {
            steps {
                withCredentials([usernamePassword(credentialsId:'mahadev',passwordVariable:'dockerpass',usernameVariable:'dockeruser')]) {
                    sh "docker login -u ${env.dockeruser} -p ${env.dockerpass}"
                    sh "docker tag pratulb/node-app ${env.dockeruser}/node-app:latest"
                    sh "docker push ${env.dockeruser}/node-app:latest"
                }
            }
        }
        stage("deploy") {
            steps {
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
