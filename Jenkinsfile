pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('gaurav-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/trediagaurav/dockerhub-push-nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                bat 'docker build -t tredia/nodeapp:test1.1.'
            }
        }
        stage('login to dockerhub') {
            steps{
                bat 'docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                bat 'docker push tredia/nodeapp:test1.1'
            }
        }
}
post {
        always {
            bat 'docker logout'
        }
    }
}

