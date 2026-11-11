pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                bat 'docker build -t event-app .'
            }
        }

        stage('Push') {
            steps {
                bat 'docker push harini2926/event-app:latest'
            }
        }

        stage('Deploy') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }
}
