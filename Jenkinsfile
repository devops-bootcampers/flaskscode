pipeline {
  agent any
  stages {
    stage('Clone Repo') {
      steps {
        echo 'Clone'
        echo 'Cloning Repo'
      }
    }

    stage('Build Image') {
      steps {
        echo 'Building Image'
      }
    }

    stage('Test Image') {
      steps {
        echo 'Testing Image'
      }
    }

    stage('Image Push') {
      steps {
        echo 'Pushing Image'
      }
    }

    stage('Update ArgoCD Manifest') {
      steps {
        echo 'Update ArgoCD Manifest'
      }
    }

  }
}