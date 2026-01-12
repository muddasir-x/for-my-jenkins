pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Pulling code from GitHub"
                git branch: 'main', url: 'https://github.com/muddasir-x/for-my-jenkins-pipelines.git'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running Docker container"
                sh '''
                docker rm -f html-site || true
                docker run -d --name html-site -p 8081:80 -v $PWD:/usr/share/nginx/html:ro nginx
                '''
            }
        }
    }
}
