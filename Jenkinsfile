pipeline {
	agent any
	// agent { docker { image 'maven:3.6.3'} }
	// agent { docker { image 'node:alpine3.17'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				//path of docker agent
				echo "PATH - $PATH"
				//env variables
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		//build jar file
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image') {
			steps {
				// old
				//"docker build -t hikiko999/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("hikiko999/currency-exchange-devops:{$env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					// (repo,id)
					docker.withRegistry('','dockerhub')
					dockerImage.push();
					dockerImage.push('latest');
				}
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