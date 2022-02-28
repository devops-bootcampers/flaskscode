pipeline {
  agent any
  stages {
    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build imagename
        }

      }
    }

  }
  environment {
    imagename = 'chielvis1/flask'
    registryCredential = 'dockerhub'
    registry = 'https://registry.hub.docker.com'
    app = ''
  }
}