pipeline {
    agent any
    parameters {
        choice(name: 'deployment', choices: 'green\nblue', description: 'Choose the blue/green deployment')
	}
    stages {
        stage('Test') {
            steps {
                sh 'echo Test'
            }
        }
        stage('Lint Dockerfile') {
            steps {
                sh 'docker run --rm -i hadolint/hadolint < Dockerfile'     
            }
        }
        stage('Build') {
            steps {
                sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 959661509556.dkr.ecr.us-east-2.amazonaws.com'
                sh 'docker build -t firstrepo .'
                sh 'docker tag firstrepo:latest 959661509556.dkr.ecr.us-east-2.amazonaws.com/firstrepo:${BUILD_NUMBER}'
                sh 'docker push 959661509556.dkr.ecr.us-east-2.amazonaws.com/firstrepo:${BUILD_NUMBER}'      
            }

	}
 }
}
