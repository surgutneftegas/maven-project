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
  }
}
    
  
