// Repo - https://github.com/asasgray2000/jenkins-devops-microservices/
// Java files located in the parent directory.

// SCRIPTED
// Stages are not required.
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Integration Test"
// 	}
// }

// DECLARATIVE
pipeline {
	agent any
 	environment {
		// Names are from the Jenkins configurations.
		// Manage Jenkins -> Global Tool Configuration
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'

		PATH = "$PATH:$dockerHome/bin:$mavenHome/bin"
	}
	stages {
		stage('Checkout') {
			steps {
				echo "Checkout Step"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_TAG - $env.BUILD_TAG"
				//Use a shell script.
				sh "mvn --version"
				sh "docker --version"
			}
		}
		stage('Compile') {
			steps {
				echo "Compile Step"
				sh "mvn clean install"
			}
		}
		stage('Test') {
			steps {
				echo "Test Step"
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
	}
	post {
		always {
			echo 'I run always.'
		}
		success {
			echo 'I run when you are successful.'
		}
		failure {
			echo 'I run when you fail.'
		}
		changed {
			echo 'I execute when the status of a build changes.'
		}

	}
}