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
          dockerImage = docker.build imagename
        }

      }
    }

    stage('Deploy Image') {
      steps {
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
            dockerImage.push('latest')

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