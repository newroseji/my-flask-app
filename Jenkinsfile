pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', credentialsId: 'jen-doc-git', url: 'https://github.com/newroseji/my-flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nirajbjk/my-flask-app:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push nirajbjk/my-flask-app:latest'
                }
            }
        }
    }
}
