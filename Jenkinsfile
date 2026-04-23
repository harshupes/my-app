pipeline {
    agent any

    environment {
        IMAGE_NAME = "harsh119184/my-app"
    }

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/harshupes/my-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Login Docker Hub') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'dockerhub-token',
                        variable: 'DOCKER_TOKEN'
                    )
                ]) {
                    sh '''
                    echo $DOCKER_TOKEN | docker login \
                    -u harsh119184 \
                    --password-stdin
                    '''
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE_NAME:latest'
            }
        }
    }
}
