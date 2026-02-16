pipeline {
    agent any
    stages {
        stage('Build Frontend') {
            steps {
                sh 'docker build -t mohanDevOpsarch/shopnow-frontend ./frontend'
            }
        }
        stage('Build Backend') {
            steps {
                sh 'docker build -t mohanDevOpsarch/shopnow-backend ./backend'
            }
        }
        stage('Push Images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push mohanDevOpsarch/shopnow-frontend'
                    sh 'docker push mohanDevOpsarch/shopnow-backend'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'helm upgrade --install shopnow ./helm/shopnow-chart -f ./helm/shopnow-chart/values.yaml'
            }
        }
    }
}
