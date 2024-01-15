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
          sh './scripts/build.sh'
        }

      }
    }

  }
  environment {
    registry = 'marcheol/cicd-hometask'
  }
}