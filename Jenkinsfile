pipeline {
  environment {
    ecrurl = "https://483034414867.dkr.ecr.us-east-1.amazonaws.com"
    ecrcredentials = "ecr:us-east-1:0535d321-41ee-44c1-aa90-71c05ec9c3f9"
    region = "us-east-1"
    jenkins_id = "0535d321-41ee-44c1-aa90-71c05ec9c3f9"
    service_name = "itamar-cer-service2"
    cluster_name = "itamar-ecr"
  } 
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
              docker.withRegistry(ecrurl, ecrcredentials) {
                  def myImage = docker.build('itamar_ecr')
                  myImage.push('latest')
                
     stage('Remove Unused docker image - main') {
      when {
      anyOf {
            branch 'main'
      }
     }
      steps{
        sh "docker rmi 'itamar_ecr':'latest'
         

      }
      } // End of remove unused docker image for mast           
                
      stage ('update service') {
        
          script {
             withAWS(region: region, credentials: jenkins_id) {
             def updateService = "aws ecs update-service --service itamar-cer-service2 --cluster itamar-ecr --force-new-deployment"
             def runUpdateService = sh(returnStdout: true, script: updateService)
             
              }
              } 
               
             
           }
        }
      }
    } 
  }
}
}  
