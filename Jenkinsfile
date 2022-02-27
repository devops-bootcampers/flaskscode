pipeline {
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git(url: 'https://github.com/devops-bootcampers/flaskmanifest.git', branch: 'master', credentialsId: 'github', poll: true)
      }
    }

    stage('Building image') {
      steps {
        script {
          app = docker.build("chielvis1/flask")
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
  }
}