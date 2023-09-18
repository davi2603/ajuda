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
    steps {
        sh 'docker push my-app'
        sh 'kubectl set image deployment/davi2603/react-app my-app=react-app'
    }
}

  }

}
