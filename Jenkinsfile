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
          def customImage = docker.build("${registry}:${env.Build_ID}").inside{
            c-> sh 'chmod +x ./scripts/build.sh;./scripts/build.sh'
          }
        }

      }
    }

  }
  environment {
    registry = 'marcheol/cicd-hometask'
  }
}