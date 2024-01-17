pipeline {
    agent any


    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker_cred')
        dockerHubUser='sravanmarolix'
        dockerHubPassword='Sravan@2023'
    }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/sravankumarsra/node-todo-cicd-master-jenkins.git', branch: 'master' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t sravanmarolix/myimage:latest'
            }
        }
        stage('Push'){
            steps{
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push sravanmarolix/myimag:latest'
                }
            }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
