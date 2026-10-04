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
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
            // First, securely log in to Docker Hub
            sh 'echo \(DOCKER_PASS | docker login -u\)DOCKER_USER --password-stdin'
            
            // Tag the image (using a variable here is best practice)
            sh 'docker tag my-devops-app $DOCKER_USER/my-devops-app:latest'
            
            // Push the image
            sh 'docker push $DOCKER_USER/my-devops-app:latest'
        }
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
