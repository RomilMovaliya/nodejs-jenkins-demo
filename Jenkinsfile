pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "nodejs-app"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("${env.DOCKER_IMAGE}:${env.BUILD_ID}")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'npm test'
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    withKubeConfig([credentialsId: 'kubeconfig']) {
                        sh 'kubectl apply -f kubernetes-deployment.yml'
                    }
                }
            }
        }
    }
}
