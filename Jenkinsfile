pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }

  // Create your credential for jenkins
  stages {
      stage('Build') {
        steps {
          sh 'pwd'
          sh 'ls -l'
          sh 'docker build -t shamal317mn/mynginx-app . '
        }
      }
    withDockerRegistry(credentialsId: 'dockerCreds', url: ' ') {
      stage('Push') {
        steps {
          sh 'docker push shamal317mn/mynginx-app'
        }
      }
    }
  }
     
  post {
    always {
      sh 'docker logout'
    }
  }
}
