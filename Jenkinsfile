pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t docker-cicd-demo:latest .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker stop docker-cicd-demo || true
                    docker rm docker-cicd-demo || true

                    docker run -d \
                        --name docker-cicd-demo \
                        -p 8081:80 \
                        docker-cicd-demo:latest
                '''
            }
        }
    }
}
