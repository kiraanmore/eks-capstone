pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Lint Dockerfile') {
            steps {
                sh 'docker run --rm -i hadolint/hadolint < Dockerfile'     
            }
        }
        stage('Build') {
            steps {
                sh 'mvn package'
                sh 'ls -a'      
            }
        }      
        stage('Push') {
            steps {
                sh 'aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 395312722260.dkr.ecr.us-west-2.amazonaws.com'
                sh 'docker build -t spring-api .'
                sh 'docker tag spring-api:latest 395312722260.dkr.ecr.us-west-2.amazonaws.com/spring-api:latest'
                sh 'docker push 395312722260.dkr.ecr.us-west-2.amazonaws.com/spring-api:latest'
            }
        }
        stage('Spring Deploy') {
            steps {
                sh 'kubectl apply -f service.yml'
                }
        }        
    }
}

