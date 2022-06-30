pipeline {
  environment {
    registry = "prathmeshrajmane/docker-test"
    registryCredential = 'dockerhub'
    dockerImage = ''

  }
 agent any
  stages {
    stage('Git Checkout') {
      steps {
        git 'https://github.com/prathmeshrajmane/cicd-web.git'
      }
    }
    stage('Docker Build') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
	 stage('Approvals') {
			steps{

				input('Test Completed ? Please provide  Approvals for Prod Release ?')
			}
		}
    stage('Deploy Push') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}
