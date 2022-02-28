pipeline {
  agent any
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }

    stage('Deploy Image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
          }
        }

        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push('latest')
          }
        }

      }
    }

    stage('Trigger Update Manifest') {
      steps {
        echo 'Triggering another job to update the Kubernetes/ArgoCD manifest file'
        script {
          build job: 'flaskmanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
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
