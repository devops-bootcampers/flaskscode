pipeline {
  agent any
  stages {
    stage('Building image') {
      steps {
        script {
          app = docker.build("chielvis1/flask")
        }

      }
    }

  }
  
      stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            app.push("$BUILD_NUMBER")
             app.push('latest')

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
