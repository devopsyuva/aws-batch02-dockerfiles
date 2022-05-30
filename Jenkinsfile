pipeline {
    agent any
    stages {
        stage('Clone repository') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        stage('Build Image') {
            steps {
                script {
                    app = docker.build("jenkins-ubuntu-nginx:latest")
                }
            }
        }
        stage('Push Image to ECR') {
            steps {
                script {
                    docker.withRegistry('https://017187748261.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:ecrsudheerdemo') { 
                    app.push()
                    }
                }
            }
        }
        stage('ECR Image Scan') {
            steps {
                script {
                    sh 'trivy image --severity CRITICAL,HIGH --exit-code=1 jenkins-ubuntu-nginx:latest'
                }
            }
        }
    }
}
