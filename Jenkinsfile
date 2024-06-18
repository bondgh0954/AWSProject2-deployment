pipeline {

  agent any



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
    stage('deploy'){
      steps{
        script{


          def dockerCmd = 'docker run -p 8080:8080 -d nanaot/java-app:newp.1'
          sshagent(['server-key']) {
              sh "ssh -o StrictHostKeyChecking=no ec2-user@3.70.229.24 ${dockerCmd}"
          }
        }
      }
    }
  }
}