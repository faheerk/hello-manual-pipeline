pipipeline {
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

    post {
        success {
            mail to: 'faheerulzaman@gmail.com',
                 subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """Good news!

The Jenkins job *${env.JOB_NAME}* (Build #${env.BUILD_NUMBER}) succeeded 🎉
Check the build details at: ${env.BUILD_URL}
"""
        }

        failure {
            mail to: 'faheerulzaman@gmail.com',
                 subject: "❌ FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """Oops 😞

The Jenkins job *${env.JOB_NAME}* (Build #${env.BUILD_NUMBER}) failed.
You can check the logs here:
${env.BUILD_URL}
"""
        }
    }
}

