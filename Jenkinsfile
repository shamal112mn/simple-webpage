pipeline {
  environment {
    registry = "shamal317mn/mynginx"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        // Clean WS before build
        cleanWs()
        git 'https://github.com/shamal112mn/simple-webpage.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push dockerhub') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }

    stage ('Build SetImage-k8s job'){
      steps {
        build wait: true, job: 'setImage-k8s', parameters: [
          string(name: 'IMAGE_TAG', value: "$BUILD_NUMBER")
        ]
      }
    }
  }
}
