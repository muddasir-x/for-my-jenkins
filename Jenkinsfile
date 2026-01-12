pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Pulling code from GitHub"
                git branch: 'main', url: 'https://github.com/muddasir-x/for-my-jenkins.git'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running Docker container"

                sh '''
                # Stop old container if exists
                docker rm -f html-site 2>/dev/null || true

                # Run Nginx container with HTML from Jenkins workspace
                docker run -d \
                    --name html-site \
                    -p 8081:80 \
                    -v $PWD:/usr/share/nginx/html:ro \
                    nginx:latest
                '''
            }
        }
    }
}
