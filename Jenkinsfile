pipeline {
  agent any
  stages {
    stage('Clone Repo') {
      parallel {
        stage('Clone Repo') {
          steps {
            git(url: 'https://github.com/devops-bootcampers/kubernetescode.git', branch: 'master', poll: true)
          }
        }

        stage('GitHub') {
          steps {
            echo 'Checking out branch'
          }
        }

      }
    }

    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build imagename
        }

      }
    }

    stage('Test Image') {
      steps {
        echo 'Testing Image'
      }
    }

    stage('Deploy Image') {
      steps {
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
            dockerImage.push('latest')

          }
        }

      }
    }

    stage('Update ArgoCD Manifest') {
      steps {
        echo 'Update ArgoCD Manifest'
      }
    }

  }
  environment {
    registry = 'https://registry.hub.docker.com'
    registryCredential = 'dockerhub'
    image_id = 'chielvis1/flask'
  }
}