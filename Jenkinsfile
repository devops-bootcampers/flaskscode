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
