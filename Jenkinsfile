#!/usr/bin/env groovy
pipeline {
  agent any
  options { skipDefaultCheckout()
            disableConcurrentBuilds()
          }

  stages {
    stage('Build Dependencies') {
      steps {
        checkout scm
        sh "npm install"
      }
    }




     stage('Package') {

      steps {
        sh  "npm run build-aws-resource"
         sh "aws cloudformation create-stack --parameters  ParameterKey=KeyName,ParameterValue=ShannonKeyPair --template-url https://s3.amazonaws.com/shannonbucket/Shannon_cloudformation_sample1 --stack-name shannon --capabilities CAPABILITY_IAM --region us-east-1"
         sh "aws cloudformation wait stack-create-complete --stack-name shannon --region us-east-1"
      }
    }


}
}
