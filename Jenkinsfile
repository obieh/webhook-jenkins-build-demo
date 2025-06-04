pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/obieh/webhook-jenkins-build-demo'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t testapp:latest .'
            }
        }

        stage('Run on Kubernetes') {
            steps {
                sh '''
                kubectl delete deployment webapp || true
                kubectl create deployment webapp --image=testapp:latest
                kubectl expose deployment webapp --type=NodePort --port=80
                '''
            }
        }
    }
}
