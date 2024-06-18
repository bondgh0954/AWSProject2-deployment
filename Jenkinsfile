pipeline {

  agent any
  tools{
    maven 'maven-3'
  }
  environment{
    IMAGE_NAME = 'nanaot/java-app:try.1'
  }

  stages{

    stage('build jar'){
      steps{
        script{
          echo 'building application jar ....'

        }
      }
    }
    stage('build image'){
      steps{
        script{
          echo 'building application image....'



          }
        }
      }
    }
    stage('deploy'){
      steps{
        script{
          echo 'deploying application to ec2 server......'
          echo 'logging in to docker private repo.....'
          withCredentials([usernamePassword(credentialsId:'dockerhub-credentials',usernameVariable:'USER',passwordVariable:'PASS')]){
            sh "echo $PASS| docker login -u $USER --password-stdin"
            def dockerCmd = "docker run -p 8080:8080 -d $IMAGE_NAME"
            sshagent(['server-key']) {
                sh "ssh -o StrictHostKeyChecking=no ec2-user@3.70.229.24 ${dockerCmd}"
            }
          }

        }
      }
    }
  }
}