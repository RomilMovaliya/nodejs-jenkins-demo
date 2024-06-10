pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/RomilMovaliya/nodejs-jenkins-demo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}

