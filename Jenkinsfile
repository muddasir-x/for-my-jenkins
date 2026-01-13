pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    
    stages {
        stage('Build') {
            steps {
                sh '''
                    docker --version
                    docker rm -f html-site || true
                    docker run -d --name html-site -p 8081:80 -v $PWD:/usr/share/nginx/html:ro nginx
                '''
            }
        }
    }
}
