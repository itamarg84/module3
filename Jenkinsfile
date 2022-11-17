pipeline {
  agent any
  stages {
    stage ('build') {
      steps {
        sh 'printenv'
        
      } 
    }    
     stage ('publish ECR') {
      steps {
          script {
              docker.withRegistry(
                  'https://483034414867.dkr.ecr.us-east-1.amazonaws.com',
                  'ecr:us-east-1:0535d321-41ee-44c1-aa90-71c05ec9c3f9') {
                  def myImage = docker.build('itamar_ecr')
                  myImage.push('latest')
           }
        }
      }
    } 
  }
}
