pipeline {
    // Agent ko Docker-in-Docker (DinD) image se set karo taaki Docker commands run ho sakein
    agent {
        docker {
            image 'docker:dind'  // Yeh image Docker daemon ke saath aati hai
            args '--privileged'   // Privileged mode required for DinD (security ke liye production mein careful raho)
        }
    }

    stages {
        stage('Checkout') {
            steps {
                // Git se code pull karo
                git branch: 'main', url: 'https://github.com/muddasir-x/for-my-jenkins.git'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                # Pehle se running container ko remove karo (agar hai toh)
                docker rm -f html-site || true
                # Nginx container run karo, port 8081 pe expose karo, aur current directory ko mount karo
                docker run -d --name html-site -p 8081:80 -v $PWD:/usr/share/nginx/html:ro nginx
                '''
            }
        }
    }

    // Optional: Post-build step to clean up (container ko stop karo job ke end pe)
    post {
        always {
            sh 'docker rm -f html-site || true'
        }
    }
}
