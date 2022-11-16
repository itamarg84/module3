pipeline {
  environment {
    imagename = "itamar-test"
    ecrurl = "https://483034414867.dkr.ecr.us-east-1.amazonaws.com"
    ecrcredentials = "ecr:us-east-1:aws-credential"
    dockerImage = ''
  } 
  agent any
  stages {
    stage('Cloning Git') {
      steps {
                checkout scm

      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
   
stage('Deploy Master Image') {
   when {
      anyOf {
            branch 'master'
      }
     }
      steps{
        script {
          docker.withRegistry(ecrurl, ecrcredentials) {     
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }

 
    stage('Remove Unused docker image - Master') {
      when {
      anyOf {
            branch 'master'
      }
     }
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

      }
    } // End of remove unused docker image for master
  }  
} //end of pipeline
