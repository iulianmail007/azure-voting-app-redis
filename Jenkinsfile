pipeline {
   agent any

   stages {
      stage('Help') {
         steps {
        powershell label: '', script: 'Write-Output "Hellp!!!"' 
         }
      }

      stage(' Verify Branch') {
         steps {
            echo "${GIT_BRANCH}" 
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

      stage('Start test app') {
         steps {
            powershell label: '', script: '''
               docker-compose up -d
               ./scripts/test_container.ps1
            '''
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            powershell label: '', script: '''
               pytest ./tests/test_sample.py
            '''
         }
      }
      stage('Stop test app') {
         steps {
            powershell label: '', script: '''
               docker-compose down
            '''
         }
      }

      // stage('Push Container') {
      //    steps {
      //    echo "$WORKSPACE"
      //    dir("$WORKSPACE/azure-vote") {
      //       script {
               

      //          docker.withRegistry('https://index.docker.io/v1/', 'DockerHub-id') {

      //          def customImage = docker.build('iulianmail007/jenkins-course:latest')

      //          /* Push the container to the custom Registry */
      //          customImage.push()

      //          }     



      //       }
      //    }
      //    }

      // }


      
 stage('Run Anchore') {
               steps {
                  powershell label: '', script: '''
                     Write-Output "blackdentech/jenkins-course" > anchore_images
                  '''
                  anchore bailOnFail: false, bailOnPluginFail: false, name: 'anchore_images'
               }
            }



   }
        
}
