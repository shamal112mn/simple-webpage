pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }

  // Create your credential for jenkins
  stages {
   withDockerRegistry(credentialsId: 'dockerCreds', url: ' ') {
     
      stage('Build') {
        steps {
          sh 'docker build -t shamal317mn/mynginx-app . '
        }
      }

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
