pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'docker-compose create'
            }
        }
 
        stage('tag images pre push') {
            steps {
                sh 'docker tag gitea/gitea:latest 537920445401.dkr.ecr.eu-west-2.amazonaws.com/gitea/gitea:latest'
                sh 'docker tag postgres:latest 537920445401.dkr.ecr.eu-west-2.amazonaws.com/gitea/postgres:latest'
            }
        }
    }
}
