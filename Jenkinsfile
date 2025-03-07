
pipeline {
    agent any

    environment {
        IMAGE_NAME = "aakritd/jenkinsdjango"
        CONTAINER_NAME = "my_django_app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/aakritd/jenkinsdjango.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                    docker run -d -p 8000:8000 --name $CONTAINER_NAME $IMAGE_NAME
                    '''
                }
            }
        }
    }
}