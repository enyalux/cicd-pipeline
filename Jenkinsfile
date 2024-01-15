pipeline {
  agent any

  def app = docker.image("${registry}:${env.BUILD_ID}")
  
  stages {
    stage('SCM checkout') {
      steps {
        script {
          checkout scm
        }

      }
    }

    stage('Build') {
      steps {
        script {
          sh 'chmod +x ./scripts/build.sh'
          sh 'scripts/build.sh'
        }

      }
    }

    stage('Test') {
      steps {
        script {
          sh 'scripts/test.sh'
        }

      }
    }

    stage('Docker Image Build') {
      steps {
        script {
          app = docker.build("${registry}:${env.Build_ID}")
        }

      }
    }

    stage('Docker Publish') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_id')
          {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
          }
        }

      }
    }

  }
  tools {
    nodejs 'nodejs'
  }
  environment {
    registry = 'marcheol/cicd-hometask'
  }
}
