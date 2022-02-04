pipeline {
  environment {
    imagename = "adithyak21/jenkins-docker"
    registryCredential = 'adithyak21'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/adithyak21/simple-docker.git', branch: 'main'])
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage =sudo docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"
      }
    }
  }
}
