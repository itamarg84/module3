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
                  'https://483034414867.dkr.ecr.us-east-1.amazonaws.com','ecr:us-east-1:0535d321-41ee-44c1-aa90-71c05ec9c3f9') {
                  def myImage = docker.build('itamar_ecr')
                  myImage.push('latest')
                
                
                
      stage ('update service') {
        steps { 
          script {
             withAWS(region: 'us-east-1', credentials: '0535d321-41ee-44c1-aa90-71c05ec9c3f9') {
             def updateService = "aws ecs update-service --service itamar-ecr-service --cluster itamar-ecr --force-new-deployment"
             def runUpdateService = sh(returnStdout: true, script: updateService)
             def serviceStable = "aws ecs wait services-stable --service $internationalService --cluster $internationalCluster"
             sh(returnStdout: true, script: serviceStable)
             // put all your slack messaging here
              }
              } catch(Exception e) {
              echo e.message.toString()
             }}
           }
        }
      }
    } 
  }
}
