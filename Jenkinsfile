pipeline {
  environment {
    registry = "prathmeshrajmane/hu"
    registryCredential = 'dockerhub'
    dockerImage = ''

  }
 agent any
  stages {
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
