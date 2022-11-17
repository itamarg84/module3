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
            sh ('aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 483034414867.dkr.ecr.us-east-1.amazonaws.com')
            sh ('docker build -t itamar_ecr .')
            sh ('docker tag itamar_ecr:latest 483034414867.dkr.ecr.us-east-1.amazonaws.com/itamar_ecr:latest')
            sh ('docker push 483034414867.dkr.ecr.us-east-1.amazonaws.com/itamar_ecr:latest')
           }
        }
     }
      
