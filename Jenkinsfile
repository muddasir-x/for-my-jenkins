pipeline {
    agent any
    
    stages {
        stage('Run Docker Container') {
            steps {
                script {
                    sh '''
                        # Use full path to docker
                        /usr/local/bin/docker --version
                        
                        # Remove existing container if any
                        /usr/local/bin/docker rm -f html-site 2>/dev/null || true
                        
                        # Run new container
                        /usr/local/bin/docker run -d \
                          --name html-site \
                          -p 8081:80 \
                          -v "$PWD":/usr/share/nginx/html:ro \
                          nginx:alpine
                        
                        # Check if running
                        sleep 2
                        /usr/local/bin/docker ps | grep html-site
                        echo "Container should be accessible at http://localhost:8081"
                    '''
                }
            }
        }
    }
}
