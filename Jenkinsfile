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

        stage('error') {
          steps {
            echo 'Checking out branch'
          }
        }

      }
    }

    stage('Build Image') {
      parallel {
        stage('Build Image') {
          steps {
            echo 'Building Image'
          }
        }

        stage('Shell') {
          steps {
            sh 'docker build -t chielvis1/flask .'
          }
        }

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
  environment {
    registry = 'https://registry.hub.docker.com'
    egistryCredential = 'dockerhub'
    image_id = 'chielvis1/flask'
  }
}