pipeline {

  environment {
    dockerimagename = "davi2603/react-app"
    dockerImage = ""
  }

  agent any

  stages {


    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'docker_hub'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

stage('Deploy') {
	agent {
		kubernetes {
			cloud 'kube'
			yaml '''
        apiVersion: v1
        kind: Pod
        metadata:
          creationTimestamp: null
          labels:
            run: teste5
          name: teste5
        spec:
          containers:
          - image: davi2603/react-app
            name: teste5

		}
	}

  }

}
