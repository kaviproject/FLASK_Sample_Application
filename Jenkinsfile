
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
                  
                 bat 'docker images -a'
                 bat 'docker image build -t smapleapplication:latest .'
                 bat 'docker tag smapleapplication docker-reg.cmog.org/smapleapplication:latest'
              
                withDockerRegistry(credentialsId: '2c6039d2-6523-4346-aef2-6047c30720a3', url: 'https://docker-reg.cmog.org') {
                     bat 'docker push docker-reg.cmog.org/smapleapplication:latest'
                }
              
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
