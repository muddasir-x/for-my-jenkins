pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Pulling code from GitHub"
                git branch: 'main', url: 'https://github.com/muddasir-x/for-my-jenkins.git'
            }
        }

        stage('Run') {
            steps {
                echo "Executing Jenkinsfile - simple test"
                sh 'echo "Hello, Jenkins is running!"'
            }
        }
    }
}
