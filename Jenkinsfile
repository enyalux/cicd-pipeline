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
          sh 'docker build -t ${registry}:${Build_ID}'
        }

      }
    }

    stage('Docker Publish') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_id')
          {
            docker.image("${registry}:${env.BUILD_ID}").push("${env.BUILD_NUMBER}")
            docker.image("${registry}:${env.BUILD_ID}").push("latest")
            //app.push("${env.BUILD_NUMBER}")
            //app.push("latest")
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