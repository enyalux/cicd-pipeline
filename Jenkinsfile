pipeline {
  agent any
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
          def customImage = docker.build("${registry}:${env.Build_ID}")
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