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
      
      stage('Docker Build') {
         steps {
            pwsh(script: 'docker images -a')

         }
      }
   }
        
}
