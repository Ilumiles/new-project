pipeline {
    agent any
	tools {
		maven 'Maven'
		}
    stages {
        stage('Build Jar') {
            steps {
                script { 
					echo " building the application"
					sh "mvn package"
				}
            }
        }
	stage('Build image') {
            steps {
		script { 
	        			echo "building the docker image"
					withCredentials([UsernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
					sh 'docker build -t ilumiles/my-repo-app:jma-2.0'
					sh "echo $PASS |docker login -u $USER –password-stdin"
					sh "docker push ilumiles/my-repo-app:jma-2.0"}
				}
                
            }
        }
		stage('Hello') {
            steps {
                echo  " deploying applications"            }
        }
    }
}

