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
                sh 'aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 813213957333.dkr.ecr.us-west-2.amazonaws.com'
                sh 'docker build -t spring-api .'
                sh 'docker tag spring-api:latest 813213957333.dkr.ecr.us-west-2.amazonaws.com/capstone:latest'
                sh 'docker push 813213957333.dkr.ecr.us-west-2.amazonaws.com/capstone:latest'
            }
        }
        stage('Spring Deploy') {
            steps {
                sh 'kubectl apply -f capstone-deployment.yml'
                }
        }        
    }
}

