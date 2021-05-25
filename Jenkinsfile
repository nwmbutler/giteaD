pipeline {
    agent any
    
    stages {
        stage('Pull TF code') {
            steps {
                git url: 'https://github.com/nwmbutler/giteaTF'
            }
        }

        stage('Build') {
            steps {
                dir('gitea2') {
                    sh 'docker-compose -f docker-compose.yml down'
                    sh 'docker-compose up --no-start'
                }
            }
        }

        stage('tag images pre push') {
            steps {
                dir('gitea2') {
                    sh 'docker tag gitea/gitea:latest 220087298643.dkr.ecr.eu-west-2.amazonaws.com/gitea:latest'
                }
            }
        }

        stage('login to ECR') {
            steps {
                dir('gitea') {
                    sh 'aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin 220087298643.dkr.ecr.eu-west-2.amazonaws.com'
                }
            }
        }

        stage('push images to ecr') {
            steps {
                dir('gitea2') {
                    sh 'docker push 220087298643.dkr.ecr.eu-west-2.amazonaws.com/gitea:latest'
                }
            }
        }

        stage('Docker cleanup') {
            steps {
                dir('gitea2') {
                    sh 'docker stop $(docker ps -aq)'
                    sh 'docker rmi $(docker images -q) --force'
                    sh 'docker system prune -f'
                }
            }
        }
    }
}
