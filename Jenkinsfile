pipeline {
	// agent any
	// agent { docker { image 'maven:3.6.3'} }
	agent { docker { image 'node:alpine3.17'} }
	stages {
		stage('Build') {
			steps {
				//sh 'mvn --version'
				//h 'node --version'
				echo "Build"
				//path of docker agent
				echo "$PATH"
				//env variables
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
		
	} 
		
	post {
		always {
			echo "I'm Awesome. I run always"
		}
		success {
			echo "I run when succes"
		}
		failure {
			echo "I run when fail"
		}
	}
}