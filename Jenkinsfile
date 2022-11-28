pipeline {
  environment {
    AWS_ACCOUNT_ID =''
    ecrcredentials = "ecr:${AWS_DEFAULT_REGION}:${JENK_ID}"
    jenkins_id = "${JENK_ID}"

  } 

   parameters {
    string (name: 'AWS_DEFAULT_REGION', defaultValue: "us-east-1")
    
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
              withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: '0535d321-41ee-44c1-aa90-71c05ec9c3f9']]) {
              def AWS_ACCOUNT_ID = sh (script: 'aws sts get-caller-identity --query "Account" --output text',returnStdout: true).trim()
              echo  "your account id is ${AWS_ACCOUNT_ID}"
              REPOSITORY_URL = "https://${AWS_ACCOUNT_ID}.dkr.ecr.us-east-1.amazonaws.com"
              docker.withRegistry("${REPOSITORY_URL}", ecrcredentials) {
                def myImage = docker.build(image_name)
                  myImage.push('latest')



    stage('Remove Unused docker image - main') {

        //sh "docker rmi -f 'latest'"
         }


    stage('Deploy'){
         
        sh 'kubectl apply -f deployment.yml'
            }



         }
        }
       }
      }
     }
    }
   }
