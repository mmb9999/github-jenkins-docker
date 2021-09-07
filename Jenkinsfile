pipeline {
	environment {
		registry = "mahesh9999/github-docker-jenkins"
		registryCredential = 'mahesh9999'
		dockerImage = ''
		dockerRunCommand = 'docker run -d -p 8080:8080 -name myapp chakilams3/github-jenkins-docker'
	}
	agent any
	stages {
		stage("Building docker image") { 
			steps {
				script {
					dockerImage = docker.build registry + ":$BUILD_NUMBER"
				}
			}
		}
		stage("Pushing image to DockerHub") { 
			steps {
				script {
					docker.withRegistry( '', registryCredential ) {
						dockerImage.push()
						dockerImage.push( 'latest' )
					}
				}
			}
		}
	}
}
