pipeline {
  environment {
    
    
    
    jenkins_id = "${JENK_ID}"
   
  } 
  agent any
  stages {
    stage ('build') {
      steps {
        sh 'printenv'
        
      } 
    }    
                  
    stage ('update service') {
        
      steps {
          script {
             withAWS(region:"${params.AWS_DEFAULT_REGION}", credentials: jenkins_id) {
               def updateService = "aws ecs update-service --service ${params.SERVICE_NAME} --cluster ${params.CLUSTER_NAME} --force-new-deployment"
               def runUpdateService = sh(returnStdout: true, script: updateService)
                }
              }
             } 
            }
           }
          }
          
