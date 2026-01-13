pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/muddasir-x/for-my-jenkins.git'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker rm -f html-site || true
                docker run -d --name html-site -p 8081:80 -v $PWD:/usr/share/nginx/html:ro nginx
                '''
            }
        }
    }
}
