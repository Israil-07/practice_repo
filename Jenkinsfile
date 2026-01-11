pipeline {
    agent any

    environment {
        // Set the host and port for the deployed app
        APP_HOST = "your.server.ip"   // Replace with your server IP or use env var
        APP_PORT = "8090"
        CONTAINER_NAME = "my_web"
    }

    stages {

        stage('Checkout Repository') {
            steps {
                echo '🔁 Checking out source code...'
                checkout scm
            }
        }

        stage('Validate Docker') {
            steps {
                echo '🛠 Validating Docker installation...'
                sh 'docker --version'
                sh 'docker compose version'
            }
        }

        stage('Remove Existing Container') {
            steps {
                script {
                    echo "🧹 Checking for existing container: ${env.CONTAINER_NAME}"
                    sh """
                    if [ \$(docker ps -aq -f name=${env.CONTAINER_NAME}) ]; then
                        echo "⚠️ Found existing container. Stopping and removing..."
                        docker stop ${env.CONTAINER_NAME} || true
                        docker rm ${env.CONTAINER_NAME} || true
                    else
                        echo "✔ No existing container found."
                    fi
                    """
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                echo "🚀 Deploying NGINX using Docker Compose..."
                sh 'docker compose up -d'
            }
        }

        stage('Verify Deployment') {
            steps {
                echo "🔍 Verifying deployment status..."
                sh 'docker ps | grep $CONTAINER_NAME'
            }
        }
    }

    post {
        success {
            echo "✅ Deployment completed successfully!"
            echo "🌐 NGINX is now accessible at: http://${APP_HOST}:${APP_PORT}"
        }
        failure {
            echo "❌ Deployment failed. Check the logs above for errors."
        }
        always {
            echo "📌 Pipeline execution finished."
        }
    }
}
