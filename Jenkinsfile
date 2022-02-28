pipeline {
  agent any
  stages {
    stage('Building image') {
      steps {
        script {
          app = docker.build imagename
        }

      }
    }

    stage('Push Image') {
      steps {
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            app.push("$BUILD_NUMBER")
            app.push('latest')

          }
        }

      }
    }

  }
  environment {
    imagename = 'chielvis1/flask'
    registryCredential = 'dockerhub'
    app = ''
  }
}