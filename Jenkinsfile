pipeline {
    agent any
    
    environment {
        AWS_REGION = "us-east-1"
        ECR_REPO = "077208284482.dkr.ecr.us-east-1.amazonaws.com/testing"
        IMAGE_TAG = "latest"
    }
    
    stages {
        
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/muddasir-x/for-my-jenkins.git'
            }
        }
        
        stage('build docker image') {
            steps {
                sh "docker build -t ${ECR_REPO}:${IMAGE_TAG} ."
            }
        }
        
        stage('test docker image') {
            steps {
                sh "docker run --rm ${ECR_REPO}:${IMAGE_TAG} echo 'test passed!'"
            }
        }
        
        stage('login aws to ecr ') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-creds']]) {
                    sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 077208284482.dkr.ecr.us-east-1.amazonaws.com"
                }
            }
        }
        
        stage('push to aws ecr') {
            steps {
                sh "docker push ${ECR_REPO}:${IMAGE_TAG}"
            }
        }
    }
    
    post {
        always {
            echo "pipelines finished"
        }
        
        success {
            echo "pipeline successfull yeahhhh let's go babay"
        }
        
        failure {
            echo "try again you failed but no die"
        }
    } 
}
