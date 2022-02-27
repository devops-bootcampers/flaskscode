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

        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push('latest')
          }
        }

      }
    }

    stage('Remove Unused docker image') {
      steps {
        sh "docker rmi $imagename:$BUILD_NUMBER"
        sh "docker rmi $imagename:latest"
        sh 'echo ${app}'
      }
    }

    stage('Trigger Update Manifest') {
      steps {
        echo 'Triggering another job to update the Kubernetes/ArgoCD manifest file'
        script {
          build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }

      }
    }

  }
  environment {
    imagename = 'chielvis/flask'
    registryCredential = 'dockerhub'
    app = ''
  }
}