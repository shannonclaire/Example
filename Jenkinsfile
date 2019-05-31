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
         aws cloudformation create-stack --parameters  ParameterKey=KeyName,ParameterValue=ShannonKeyPair --template-url 'https://s3.console.aws.amazon.com/s3/buckets/shannonbucket' --stack-name shannon --capabilities CAPABILITY_IAM --region us-east-1
         aws cloudformation wait stack-create-complete --stack-name shannon --region us-east-1
      }
    }


}
}
