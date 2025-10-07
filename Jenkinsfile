pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker image...'
                    sh 'docker build -t hello-manual-image .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    echo 'Stopping old container (if any)...'
                    sh 'docker stop hello-manual-container || true'
                    sh 'docker rm hello-manual-container || true'
                    echo 'Running new container...'
                    sh 'docker run -d -p 8085:80 --name hello-manual-container hello-manual-image'
                }
            }
        }
    }
}
