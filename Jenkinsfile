pipeline {
    agent any
    stages{
        stage('Code'){
            steps{
               git url: 'https://github.com/LondheShubham153/node-todo-cicd.git', branch: 'master'  
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t sravanmarolix/test:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'pass', usernameVariable: 'user')]) {
                 sh "docker login -u ${env.user} -p ${env.pass}"
                 sh 'docker push sravanmarolix/test:latest'
}
                }
            }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
