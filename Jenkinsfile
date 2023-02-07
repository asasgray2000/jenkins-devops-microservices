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
	//agent any
	agent { docker { image 'maven:3.6.3' } }
	stages {
		stage('Build') {
			steps {
				echo "Build Step"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_TAG - $env.BUILD_TAG"
				// Use a shell script.
				sh "mvn --version"
			}
		}
		stage('Test') {
			steps {
				echo "Test Step"
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