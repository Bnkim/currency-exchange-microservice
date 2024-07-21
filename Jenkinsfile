pipeline {
	agent { docker { image 'maven:3.6.3'} }
	//agent any

	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages{
		stage('Checkout') {
			steps {
				//sh "mvn --version"
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

		stage('Package') {
			steps {
					sh "mvn package -DskipTests"
				}
			}

		stage('Build Docker Image'){
				steps{
					//"docker build -t unkim/currency-exchange-devops:$env.BUILD_TAG"
					script {
						dockerImage = docker.build("unkim/currency-exchange-devops:${env.BUILD_TAG}")
					}
				}
			}

			stage('Push Docker Image'){
				steps{
					script{
					 	docker.withRegistry('', 'dockerHub') {
							dockerImage.push();
							dockerImage.push('latest');
						}
					}
				}
			}
	}
}
