pipeline {
    agent any

    stages {

        stage('Verify git repo') {
            steps {
                echo 'Git repo cloned successfully'
            }
        }

        stage('Check Docker & Run Container') {
            steps {
                sh 'docker --version'
                sh 'docker compose up -d'
            }
        }

        stage('Check the Status') {
            steps {
                sh 'docker images'
                sh 'docker ps | grep my_web'
            }
        }
    }

    post {
        success {
            echo "✅ NGINX deployed successfully using Jenkins"
        }
        failure {
            echo "❌ Deployment failed"
        }
    }
}
