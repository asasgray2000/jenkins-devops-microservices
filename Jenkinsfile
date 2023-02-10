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
				sh "echo Git env variables"
				sh "printenv | grep Git"
				sh "printenv | grep cert"
				sh "pwd"
				sh "ls -la /"
				sh "whoami"
				//sh "find /| grep pem"
				sh "find /certs/client"
				sh "echo end"
			}
		}
		//This is done inside the Jenkins Docker Container.
		stage('Compile') {
			steps {
				echo "Compile Step"
				sh "mvn clean compile"
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
		stage('Build Docker Image') {
			steps {
				echo "Build Docker Image"
				sh "export DOCKER_CERT_PATH=/certs/client"
				sh "echo $DOCKER_CERT_PATH"
				sh "cp -f /certs/client/* C:/Program Files/Git/certs/client/"
				sh "docker build -t asasgray/currency-exchange-devops:$env.BUILD_TAG ."
				// script {
				// 	// arg1=default to dockerhub repo.
				// 	// arg2=Id set in Global Credentials.
				// 	dockerImage = docker.build("asasgray/currency-exchange-devops:$env.BUILD_TAG")
				// }
			}
		}
		// stage('Push Docker Image') {
		// 	steps {
		// 		echo "Push Docker Image"
		// 		script {
		// 			// arg1=default to dockerhub repo.
		// 			// arg2=Id set in Global Credentials.
		// 			docker.withRegistry('', 'dockerhub') {
		// 				dockerImage.push();
		// 				dockerImage.push('latest');
		// 			}
		// 		}
		// 	}
		// }
		stage('Package') {
			steps {
				echo "Package Step"
				sh "mvn package -DskipTests"
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