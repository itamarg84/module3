
pipeline {
  environment {
        AWS_ACCESS_KEY_ID = 'AKIAXA5YYH4J3W7YI4UK'
        AWS_SECRET_ACCESS_KEY = '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'
        AWS_DEFAULT_REGION = 'us-east-1'
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
        withEnv (["AWS_ACCESS_KEY_ID-${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY-${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION-${env.AWS_DEFAULT_REGION}"]) {
          sh 'docker login -u AWS -p $(aws ecr get-login-password --region us-east-1 ) 483034414867.dkr.ecr.us-east-1.amazonaws.com/itamar_ecr'
          sh 'docker build -t itamar_ecr .'
          sh 'docker tag itamar_ecr:latest 483034414867.dkr.ecr.us-east-1.amazonaws.com/itamar_ecr:latest'
          sh 'docker push 483034414867.dkr.ecr.us-east-1.amazonaws.com/itamar_ecr:latest'
        }
      }
    }
  }
}
