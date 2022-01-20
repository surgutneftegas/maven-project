pipeline {
  agent any
  triggers {
    pollSCM('*/5 * * * *')
  }
  stages{
       stage ('Build'){
        steps {
          sh 'mvn clean package'
        }
        post {
          success {
            echo 'Archiving ...'
            archiveArtifacts artifacts:'**/target/*.war'  
          }
        }
       }
       stage ('Deployments') {
          parellel {
            stage ('Deploy to staging') {
              steps {
              sh 'copy **/target/*.war /home/ubuntu/tomcat-stage/webapps'
              }     
            }
            stage ('Deploy in prod') {
              steps {
              timeout(time:5, unit:'DAYS') {
              input message:'Approve Prod deployment?'
              }
              sh 'copy **/target/*.war /home/ubuntu/tomcat-prod/webapps
              }
            }
          }
      }
  }
}
    
  
