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

        stage('') {
          steps {
            echo 'Checking out branch'
          }
        }

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