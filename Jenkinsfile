pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('gaurav-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/ravdy/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                bat 'docker build -t valaxy/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                bat 'docker push valaxy/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            bat 'docker logout'
        }
    }
}

