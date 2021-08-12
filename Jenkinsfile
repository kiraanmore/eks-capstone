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
                sh 'echo Build Stage'
                sh 'ls -a'      
            }

	}
 }
}
