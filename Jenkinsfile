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
            // Direct login command bina echo aur pipe ke
            sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
            
            sh 'docker tag my-devops-app $DOCKER_USER/my-devops-app:latest'
            sh 'docker push $DOCKER_USER/my-devops-app:latest'
        }
    }
}
        stage('Deploy App') {
    steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
            // Pehle purana container remove karein
            sh 'docker rm -f my-app-container'
          
            // Naya container run karein (Yaha sahi image naam use kiya hai)
            sh 'docker run -d -p 80:80 --name my-app-container $DOCKER_USER/my-devops-app:latest'
        }
    }
 }
 }
 }
