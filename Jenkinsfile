pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'docker-compose -f docker-compose.yml down'
                sh 'docker-compose up --no-start'
            }
        }

        stage('tag images pre push') {
            steps {
                sh 'docker tag gitea/gitea:latest 537920445401.dkr.ecr.eu-west-2.amazonaws.com/gitea:latest'
                sh 'docker tag postgres:latest 537920445401.dkr.ecr.eu-west-2.amazonaws.com/postgres:latest'
            }
        }

        stage('login to ECR') {
            steps {
                sh 'aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin 537920445401.dkr.ecr.eu-west-2.amazonaws.com'
            }
        }

        stage('push images to ecr') {
            steps {
                sh 'docker push 537920445401.dkr.ecr.eu-west-2.amazonaws.com/gitea:latest'
                sh 'docker push 537920445401.dkr.ecr.eu-west-2.amazonaws.com/postgres:latest'
            }
        }

        stage('Docker cleanup') {
            steps {
                sh 'docker stop $(docker ps -aq)'
                sh 'docker rmi $(docker images -q) --force'
                sh 'docker system prune -f'
            }
        }
    }
}
