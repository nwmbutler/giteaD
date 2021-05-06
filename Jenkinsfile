pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'docker-compose create'
            }
        }
 
        stage('Image push to ECR') {
            steps {
                script {
                    docker.withRegistry('537920445401.dkr.ecr.eu-west-2.amazonaws.com', 'ecr:eu-west-2:${ecs-access}') {
                    docker.image('ecsgitea').push('latest')
                    }
                }
            }
        }
    }
}
