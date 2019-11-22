pipeline{
   agent any
   stages{
   stage('SCM Checkout'){
     git 'https://github.com/sudharsansadasivam/my-app-2'
   }
   stage('Compile-Package'){
      echo "Compile Stage Passed"
      // Get maven home path
      //def mvnHome =  tool name: 'maven-3', type: 'maven'   
      //sh "${mvnHome}/bin/mvn package"
   }
   }
   /*
   stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'maven-3', type: 'maven'
        withSonarQubeEnv('sonar-6') { 
          sh "${mvnHome}/bin/mvn sonar:sonar"
        }
    }
     
   stage("Quality Gate Status Check"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {

                    echo "Quality Gate  Failure!"
                 sh """
                    curl "https://api.github.com/repos/sudharsansadasivam/my-app-2/statuses/env.GIT_COMMIT?access_token=fc12e2cffd299cd8aec3b09b6dd0d94d41e9be37" \
                    -H "Content-Type: application/json" \
                    -X POST \
                    -d "{\"state\": \"failure\",\"context\": \"continuous-integration/jenkins\", \"description\": \"Jenkins\", \"target_url\": \"http://ec2-13-58-34-76.us-east-2.compute.amazonaws.com/job/Jenkins_c/env.BUILD_NUMBER/console\"}"
                  """  

              }
             if (qg.status != 'FAILURE') {

                    echo "Quality Gate  Success!"
                    sh """
                    curl "https://api.github.com/repos/sudharsansadasivam/my-app-2/statuses/env.GIT_COMMIT?access_token=fc12e2cffd299cd8aec3b09b6dd0d94d41e9be37" \
                    -H "Content-Type: application/json" \
                    -X POST \
                    -d "{\"state\": \"success\",\"context\": \"continuous-integration/jenkins\", \"description\": \"Jenkins\", \"target_url\": \"http://ec2-13-58-34-76.us-east-2.compute.amazonaws.com/job/Jenkins_c/env.BUILD_NUMBER/console\"}"
                     """
              }
          }
      }    
   
  /* 
   stage('Email Notification'){
      mail bcc: '', body: '''Hi Welcome to jenkins email alerts
      Thanks
      Sudharsan''', cc: '', from: '', replyTo: '', subject: 'Jenkins Job', to: 'sudharsansadasivam@gmail.com'
   }
   */
   /*
   stage('Slack Notification'){
       slackSend baseUrl: 'https://hooks.slack.com/services/',
       channel: '#jenkins-pipeline',
       color: 'good', 
       message: 'Welcome to Jenkins, Slack!', 
       teamDomain: 'Devops',
       tokenCredentialId: 'slack-ID'
   }*/

}


