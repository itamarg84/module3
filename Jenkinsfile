pipeline {
  environment {
    ecrurl = "https://483034414867.dkr.ecr.us-east-1.amazonaws.com"
    ecrcredentials = "ecr:us-east-1:0535d321-41ee-44c1-aa90-71c05ec9c3f9"
    region = ${AWS_DEFAULT_REGION}
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
       
        sh "docker rmi 'itamar_ecr':'latest'"
         }
                   
                
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
