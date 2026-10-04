pipeline {
    agent any
    stages {
        stage('Build Image') {
            steps {
                sh 'docker build -t my-devops-app .'
            }
        }
        stage('Deploy App') {
            steps {
                sh 'docker rm -f my-app-container || true'
                sh 'docker run -d -p 80:80 --name my-app-container my-devops-app'
            }
        }
    }
}
