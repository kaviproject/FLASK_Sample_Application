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
               cd FLASK_Sample_Application/
               docker images -a
               docker image build -t smapleapplication:latest .
               docker tag smapleapplication docker-reg.cmog.org/smapleapplication:latest
               docker push docker-reg.cmog.org/smapleapplication:latest
               docker images -a
               cd ..
            """)
         }
      }
   }
}