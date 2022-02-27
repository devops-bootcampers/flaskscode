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

    stage('Build Image') {
      parallel {
        stage('Build Image') {
          steps {
            echo 'Building Image'
          }
        }

        stage('Shell') {
          steps {
            sh 'docker build -t ${image_id} .'
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
      parallel {
        stage('Image Push') {
          steps {
            echo 'Pushing Image'
          }
        }

        stage('Tagging and Pushing') {
          steps {
            sh '\'docker tag ${image_id} ${image_id}:${BUILD_NUMBER}\''
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
    egistryCredential = 'dockerhub'
    image_id = 'chielvis1/flask'
  }
}