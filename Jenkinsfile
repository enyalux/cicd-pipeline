pipeline {
  agent any
  stages {
    stage('SCM checkout') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:${env.Build_ID}")
        }

      }
    }

    stage('Build') {
      steps {
        script {
          docker.image("${registry}:${env.BUILD_ID}").inside{
            c-> sh 'scripts/build.sh'}
          }

        }
      }

    }
    environment {
      registry = 'marcheol/cicd-hometask'
    }
  }