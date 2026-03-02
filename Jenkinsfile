pipeline {
    agent any

    environment {
        IMAGE = "akilapradeep/jenkin-deploy-methods"
        CONTAINER = "jenkins-container"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/akilagrepo/jenkindeploy.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

        stage('Docker Login') {
            steps {
                withDockerRegistry([credentialsId: 'jenkin-deploy-token', url: '']) {
                    sh 'docker push $IMAGE'
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f $CONTAINER || true
                docker pull $IMAGE
                docker run -d -p 3000:3000 --name $CONTAINER $IMAGE
                '''
            }
        }
    }
}