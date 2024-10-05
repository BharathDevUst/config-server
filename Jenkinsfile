pipeline {
	agent any
	tools {
		maven "maven-3.9.9"
		jdk "java-17"
	}
	stages {
		stage('Clone'){
			steps {
			    git url: "https://github.com/bharathdevust/config-server.git",
			    branch: "master"
			}
		}
		stage('Build'){
		    steps {
			    bat "mvn clean install -DskipTests"
			}
		}
		stage('Test'){
			steps {
			    bat "mvn test"
            }
		}
		stage('Deploy') {
			steps {
			    bat "docker rm -f config-server"
			    bat "docker rmi -f config-image"
			    bat "docker build -t config-image ."
                bat "docker run -p 8088:8088 -d --name config-server config-image"
            }
		}
	}
}
