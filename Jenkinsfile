pipeline {

    agent any

    stages {

        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mywebapp:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop mycontainer || true
                docker rm mycontainer || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                docker run -d \
                --name mycontainer \
                -p 80:80 \
                mywebapp:latest
                '''
            }
        }

    }

}
