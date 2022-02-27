pipeline {
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git(url: 'https://github.com/devops-bootcampers/kubernetescode.git', branch: 'master', credentialsId: 'github')
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

      }
    }

    stage('Remove Unused docker image') {
      steps {
        sh "docker rmi $imagename:$BUILD_NUMBER"
        sh "docker rmi $imagename:latest"
      }
    }

  }
  environment {
    imagename = 'chielvis/flask'
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
}