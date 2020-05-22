pipeline {
   agent {label 'LABELL'}

   stages {
      stage('Verify Branch') {
         steps {
            echo "env.BRANCH_NAME"
         }
      }
      stage('Docker Build') {
         steps {
            pwsh(script: 'docker images -a')
            pwsh(script: """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """)
         }
      }
   }
        
}
