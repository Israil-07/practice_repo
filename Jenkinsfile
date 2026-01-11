pipeline {
    agent any

    stages{

        stage('Verify git repo'){
            step {
                echo 'Git repo clone'  
            }
        }

        stage('check and run docker'){
            step {
                sh 'docker --version'
                sh 'docker compose -d up'
            }
        }

        stage(check the status){
            step {
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
