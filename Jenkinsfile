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
        
        sh "pwd"
        sh "aws s3 cp server.js s3://shannonbucket/server.js"
         sh "aws cloudformation create-stack --parameters  ParameterKey=KeyName,ParameterValue=ShannonKeyPair --template-url https://s3.amazonaws.com/shannonbucket/Shannon_cloudformation_sample1 --stack-name shannon1 --capabilities CAPABILITY_IAM --region us-east-1"
         sh "aws cloudformation wait stack-create-complete --stack-name shannon1 --region us-east-1"
      }
    }


}
}
