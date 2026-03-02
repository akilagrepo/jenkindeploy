pipeline {
    agent any

    environment {
        IMAGE = "demo-app"
        CONTAINER = "demo-container"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/demo-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f $CONTAINER || true
                docker run -d -p 3000:3000 --name $CONTAINER $IMAGE
                '''
            }
        }
    }
}