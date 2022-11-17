pipeline {
  environment {
    registry = '483034414867.dkr.ecr.us-east-1.amazonaws.com/itamar_ecr'
    registryCredential = '0535d321-41ee-44c1-aa90-71c05ec9c3f9L'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = def myImage = docker.build('itamar_ecr')
        }
      }
    }
    stage('Deploy image') {
        steps{
            script{
                docker.withRegistry("https://" + registry, "ecr:us-east-1:" + registryCredential) {
                    dockerImage.push()
                }
            }
        }
    }
  }
}
