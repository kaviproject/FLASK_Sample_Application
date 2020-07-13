
pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
           // checkout 
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
            """)
         }
      }
      stage('Approve PROD Deploy') {
         when {
            expression {
            env.GIT_BRANCH == 'origin/master'
            //return env.BRANCH_NAME != 'master';
            }
            //branch 'origin/master'
         }
         options {
            timeout(time: 1, unit: 'HOURS') 
         }
         steps {
            input message: "Can I Deploy into PROD?"
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
     stage('Deploy')
      {
      environment {
       registry = "magalixcorp/k8scicd"
         }
         steps{
            script
            {
             def image_id = registry + ":$BUILD_NUMBER"
             echo '$image_id'
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