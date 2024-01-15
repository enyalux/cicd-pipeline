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
          docker.image("${registry}:${env.BUILD_ID}").inside{
            c-> sh 'chmod +x ./scripts/build.sh; scripts/build.sh'
          }
        }

      }
    }

    stage('Test') {
      steps {
        script {
          docker.image("${registry}:${env.BUILD_ID}").inside{
            c-> sh 'scripts/test.sh'
          }
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