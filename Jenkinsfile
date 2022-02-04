pipeline {
  agent { label 'agent' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }

  // Create your credential for jenkins
  environment {
    DOCKERHUB_CREDENTIALS = credentials('shamal317mn-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t shamal317mn/simple-webpage Dockerhub-pushImage/'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push shamal317mn/simple-webpage'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
