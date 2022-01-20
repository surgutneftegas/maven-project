pipeline {
  agent any
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
       stage ('Deploy in staging') {
          steps {
            build job:'deploy_to_staging'
          }     
       }
       stage ('Deply in prod') {
         steps {
           timeout(time:5, untill:'DAYS')
             input message:'Approve Prod deployment?'
           build job:'deploy_to_prod'
         }
       }
  }
}
    
  
