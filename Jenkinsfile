pipeline {

  agent any
  tools{
    maven 'maven-3'
  }
  environment{
    IMAGE_NAME = 'nanaot/java-app:aws4.1'
  }

  stages{

    stage('build jar'){
      steps{
        script{
          echo 'building application jar ....'
          sh 'mvn package'
        }
      }
    }
    stage('build image'){
      steps{
        script{
          echo 'building application image....'
          sh "docker build -t $IMAGE_NAME ."
          echo 'logging in to docker private repo.....'
          withCredentials([usernamePassword(credentialsId:'dockerhub-credentials',usernameVariable:'USER',passwordVariable:'PASS')]){
            sh "echo $PASS| docker login -u $USER --password-stdin"
            sh "docker push $IMAGE_NAME"
          }
        }
      }
    }
    stage('deploy'){
      steps{
        script{
          echo 'deploying application to ec2 server......'
        }
      }
    }
  }
}