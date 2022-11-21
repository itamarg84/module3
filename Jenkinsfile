pipeline {
  environment {
    ecrurl = "https://${AWS_ACCOUNT_ID}.dkr.ecr.us-east-1.amazonaws.com"
    ecrcredentials = "ecr:${AWS_DEFAULT_REGION}:${JENK_ID}"
    region = "${AWS_DEFAULT_REGION}"
    jenkins_id = "${JENK_ID}"
    service_name = "${SERVICE_NAME}"
    cluster_name = "${CLUSTER_NAME}"
    image_name   = "${IMAGE_NAME}"
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
                def myImage = docker.build('${image_name}')
                  myImage.push('latest')
                
     
      
      stage('Remove Unused docker image - main') {
       
        sh "docker rmi '${image_name}':'latest'"
         }
                   
                
      stage ('update service') {
        
          script {
             withAWS(region: region, credentials: jenkins_id) {
               def updateService = "aws ecs update-service --service ${service_name} --cluster ${cluster_name} --force-new-deployment"
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
