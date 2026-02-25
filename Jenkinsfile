pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Run Backend Containers') {
            steps {
                sh '''
                docker rm -f backend1 backend2 || true
                docker run -d --name backend1 backend-app
                docker run -d --name backend2 backend-app
                '''
            }
        }

        stage('Run NGINX') {
            steps {
                sh '''
                docker rm -f nginx || true
                docker build -t nginx-app nginx
                docker run -d -p 80:80 --name nginx nginx-app
                '''
            }
        }
    }
}