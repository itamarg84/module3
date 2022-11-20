pipeline {
  agent any
  environment {
    AWS_ACCOUNT_ID= '483034414867'
    AWS_DEFAULT_REGION= 'us-east-1'
    AWS_CRE= '0535d321-41ee-44c1-aa90-71c05ec9c3f9'
    SERVICE_NAME = 'itamar-cer-service'
    CLUSTER_NAME = 'itamar-ecr'
  }
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
                'https://${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com','ecr:${AWS_DEFAULT_REGION}:${AWS_CRE}') {
                  def myImage = docker.build('itamar_ecr')
                  myImage.push('latest')
                
                
                
      stage ('update service') {
        
          script {
             withAWS('region:${AWS_DEFAULT_REGION}', credentials: '${AWS_CRE}') {
               def updateService = "aws ecs update-service --service ${SERVICE_NAME} --cluster ${CLUSTER_NAME} --force-new-deployment"
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
