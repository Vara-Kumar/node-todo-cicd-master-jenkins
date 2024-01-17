pipeline {
    agent any
    environment {
        MY_VARIABLE = 'varakumar/node-todo-test:latest'
    }
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/Vara-Kumar/node-todo-cicd-master-jenkins.git', branch: 'master' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build -t ${MY_VARIABLE} .'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    sh "docker login -u ${env.user} -p ${env.pass}"
                    sh 'docker push ${MY_VARIABLE}'
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
