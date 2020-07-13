
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
               docker.withServer('tcp://172.17.105.12:2375') {
               //bat 'docker images -a'
               powershell(script: """
               docker images -a
               docker image build -t smapleapplication:latest .
               docker tag smapleapplication docker-reg.cmog.org/smapleapplication:latest
               docker push docker-reg.cmog.org/smapleapplication:latest
            """)
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
