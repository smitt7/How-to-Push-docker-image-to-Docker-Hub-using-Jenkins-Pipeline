pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerHub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/smitt7/nodeapp_test.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t smitt/nodeapp_test:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push smitt/nodeapp_test:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
