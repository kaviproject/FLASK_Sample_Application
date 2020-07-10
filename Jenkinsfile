/*docker image build -t smapleapplication:latest .
docke tag smapleapplication docker-reg.cmog.org/smapleapplication:latest
docker push docker-reg.cmog.org/smapleapplication:latest*/
pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
            powershell(script: 'docker images -a')
            powershell(script: """
               docker images -a
               docker image build -t smapleapplication:latest .
               docker tag smapleapplication docker-reg.cmog.org/smapleapplication:latest
               docker push docker-reg.cmog.org/smapleapplication:latest
               docker images -a
               cd ..
            """)
         }
      }
      stage('Approve PROD Deploy') {
         when {
            branch 'origin/master'
         }
         options {
            timeout(time: 1, unit: 'HOURS') 
         }
         steps {
            input message: "Deploy?"
         }
         post {
            success {
               echo "Production Deploy Approved"
            }
            aborted {
               echo "Production Deploy Denied"
            }
         }
      }
       
   }
   post {
        always {
            emailext body: 'Pipeline code testing with email service', recipientProviders: [
                [$class: 'DevelopersRecipientProvider'],
                [$class: 'RequesterRecipientProvider']
            ], subject: 'PipelineScript Email Testing'
        }
    }
}