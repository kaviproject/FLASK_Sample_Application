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
   }
}