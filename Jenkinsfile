

pipline {
  agent any
  environment {
        LC_ALL = 'en_US.'
        LANG    = 'en_US.UTF-8'
        LANGUAGE = 'en_US.UTF-8'
    }
  stages {
    stage ('build') {
      steps {
        sh 'printenv'
        
      } 
    }    
    stage ('publish ECR') {
      steps {
        withenv (["AWS_ACCESS_KEY_ID-${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY_ID-${env.AWS_SECRET_ACCESS_KEY_ID}", "AWS_DEFAULT_REGION-${env.AWS_DEFAULT_REGION}"]) {
          sh 'docker login -u AWS -p $(aws ecr-public get-login-password --region us-east-1) 483034414867.dkr.ecr.us-east-1.amazonaws.com/itamar_ecr'
          sh 'docker build -t itamar_ecr . '
          sh 'docker tag itamar_ecr:""$BUILD_ID""'
          sh 'docker push 483034414867.dkr.ecr.us-east-1.amazonaws.com/itamar_ecr/itamar_ecr:""$BUILD_ID""'
        }
      }
    }
  }
}
