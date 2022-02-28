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

    stage('Image Build') {
      steps {
        echo 'Building Image'
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
          }
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