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
	stages {
		stage('Build') {
			steps {
				echo "Build Step"
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

	}
}