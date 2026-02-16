pipeline {
    agent any
    stages {
        stage('Build Frontend') {
            steps {
                sh 'docker build -t kumarDevOps/shopnow-frontend ./frontend'
            }
        }
        stage('Build Backend') {
            steps {
                sh 'docker build -t kumarDevOps/shopnow-backend ./backend'
            }
        }
        stage('Push Images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push kumarDevOps/shopnow-frontend'
                    sh 'docker push kumarDevOps/shopnow-backend'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'helm upgrade --install shopnow ./shopnow-chart -f ./shopnow-chart/values.yaml'
            }
        }
    }
}
