
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
            script{
               docker.withserver('tcp://172.17.105.12:2375', '5f8f9d48-44d9-4872-b854-f8f6cff73aea') {
              bat 'docker images -a'
             }
            }
            
            /*powershell(script: 'docker images -a')
            powershell(script: """
               docker images -a
               docker image build -t smapleapplication:latest .
               docker tag smapleapplication docker-reg.cmog.org/smapleapplication:latest
               docker push docker-reg.cmog.org/smapleapplication:latest
            """)*/
         }
      }
     
    }
}
