pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'docker compose up --no-start'
            }
        }
 
        stage('Image push to ECR') {
            steps {
                script {
                    docker.withRegistry('https://1234567890.dkr.ecr.us-east-1.amazonaws.com', 'ecr:eu-west-2:ecs-access') {
                    docker.image('gitea/gitea').push('latest')
                    }
                }
            }
        }
    }
}
