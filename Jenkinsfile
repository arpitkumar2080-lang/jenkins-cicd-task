pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/arpitkumar2080-lang/jenkins-cicd-task.git'
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t my-devops-app .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                // Replace '' with your actual Docker Hub username
                sh 'docker tag my-devops-app /my-devops-app:latest'
                sh 'docker push /my-devops-app:latest'
            }
        }
        stage('Deploy App') {
            steps {
                sh 'docker rm -f my-app-container || true'
                sh 'docker run -d -p 80:80 --name my-app-container /my-devops-app:latest'
            }
        }
    }
}
