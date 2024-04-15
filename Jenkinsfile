pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/kumarvmadhu/nodeapp_test.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t kumarvmadhu/nodeapp_test:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
				sh "docker rmi kumarvmadhu/nodeapp_test:latest"
			}
		}

		stage('Push') {

			steps {
				
				sh 'docker push kumarvmadhu/nodeapp_test:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
