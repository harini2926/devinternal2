
pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                bat 'docker build -t harini2926/event-app:latest .'
            }
        }

        stage('Login and Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DH_USER',
                    passwordVariable: 'DH_PASS'
                )]) {
                    bat '''
                    echo %DH_PASS% | docker login -u %DH_USER% --password-stdin
                    docker push harini2926/event-app:latest
                    '''
                }
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
