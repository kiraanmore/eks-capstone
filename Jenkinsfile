pipeline {
    agent any
    parameters {
        choice(name: 'deployment', choices: 'green\nblue', description: 'Choose the blue/green deployment')
	}
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
 }
}
