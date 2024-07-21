pipeline {
	//agent { docker { image 'maven:3.6.3'} }
	agent any
	stages{
		stage('Build') {
			steps {
				sh "mvn --version"
				echo "Build"
			}	
		}
		stage('Compile'){
			steps{
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
	}
}
