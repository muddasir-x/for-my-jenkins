pipeline {
    agent any
    
    environment {
        AWS_ECR_REPO = "077208284482.dkr.ecr.us-east-1.amazonaws.com/testing"
        AWS_REGION = "us-east-1"
        IMAGE_TAG = "v18"
    }
    
    stages {
        
        stage('checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/muddasir-x/for-my-jenkins.git'
            }
        }
        
        stage('build docker image') {
            steps {
                sh "docker build -t ${AWS_ECR_REPO}:${IMAGE_TAG} ."
            }
        }
        
        stage('docker image test') {
            steps {
                sh "docker run --rm ${AWS_ECR_REPO}:${IMAGE_TAG} echo 'test passed!'"
            }
        }
        
        stage('aws login into ecr') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-creds']]) {
                    sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 077208284482.dkr.ecr.us-east-1.amazonaws.com"
                }
            }
        }
        
        stage('docker image push ecr') {
            steps {
                sh "docker push ${AWS_ECR_REPO}:${IMAGE_TAG}"
            }
        }
    }
    
    post {
        always {
            echo "pipelines finished"
        }
        
        success {
            echo "pipelines successfull!! yeahhh let'sgo baby"
        }
        
        failure {
            echo "pipelines failed its okay try againg boy"
        }
    }
}
