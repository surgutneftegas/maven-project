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
          parallel {
            stage ('Deploy to staging') {
              steps {
              sh 'sudo cp **/target/*.war /home/ubuntu/tomcat-stage/webapps'
              }     
            }
            stage ('Deploy in prod') {
              steps {
              sh 'sudo cp **/target/*.war /home/ubuntu/tomcat-prod/webapps'
              }
            }
          }
      }
  }
}
    
  
