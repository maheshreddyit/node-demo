pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('maheshr8050-docker')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/maheshreddyit/node-demo/tree/main'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t maheshr8050/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push maheshr8050/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

