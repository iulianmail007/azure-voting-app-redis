pipeline {
   agent any

   stages {
      stage('Help') {
         steps {
        powershell label: '', script: 'Write-Output "Hellp!!!"' 
         }
      }

      stage('Branch') {
         steps {
            echo "${GIT_BRANCH}" 
         }
      }
      
      stage('Docker Info') {
         steps {
            powershell label: '', script: 'docker images -a'

         }
      }
      
       stage('Docker Build') {
         steps {
            powershell label: '', script: '''cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..'''
         }
      }
      
   }
        
}
