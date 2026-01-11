pipeline {
    agent any

    stages{

        stage('Verify git repo'){
            steps {
                echo 'Git repo clone'  
            }
        }

        stage('check and run docker'){
            steps {
                sh 'docker --version'
                sh 'docker compose -d up'
            }
        }

        stage('check the status'){
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
