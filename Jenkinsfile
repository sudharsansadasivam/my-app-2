pipeline{
   agent any
   tools {
        maven "3.6.3" // You need to add a maven with name "3.6.0" in the Global Tools Configuration page
    }
   stages{
   stage('SCM Checkout'){
      
      steps{
            echo "SCM Checkout Started"
	        script{
		            git 'https://github.com/sudharsansadasivam/my-app-2'
	            }
            echo "SCM Checkout Completed"
      }
   }
   stage('Compile-Package'){
      steps{
         script{
	 sh "mvn -version"
         sh "mvn clean install"
         sh "mvn package"
	 echo "Compile Stage Passed"
	 }
   }
   }
   
   stage('SonarQube Analysis') {
      steps{
         script{
         
        withSonarQubeEnv('sonar') { 
          sh "mvn sonar:sonar"
	}
        }
        }
    }
     
   stage("Quality Gate Status Check"){
      steps{
          timeout(time: 1, unit: 'HOURS') {
             script{
                def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                    echo "Quality Gate  Failure!"
                 sh """
                    curl "https://api.github.com/repos/sudharsansadasivam/my-app-2/statuses/env.GIT_COMMIT?access_token=fc12e2cffd299cd8aec3b09b6dd0d94d41e9be37" \
                    -H "Content-Type: application/json" \
                    -X POST \
                    -d "{\"state\": \"failure\",\"context\": \"continuous-integration/jenkins\", \"description\": \"Jenkins\", \"target_url\": \"http://ec2-3-10-173-226.eu-west-2.compute.amazonaws.com/job/Jenkins_c/env.BUILD_NUMBER/console\"}"
                  """ 
              }
              
             if (qg.status != 'FAILURE') {

                    echo "Quality Gate  Success!"
                    sh """
                    curl "https://api.github.com/repos/sudharsansadasivam/my-app-2/statuses/env.GIT_COMMIT?access_token=fc12e2cffd299cd8aec3b09b6dd0d94d41e9be37" \
                    -H "Content-Type: application/json" \
                    -X POST \
                    -d "{\"state\": \"success\",\"context\": \"continuous-integration/jenkins\", \"description\": \"Jenkins\", \"target_url\": \"http://ec2-3-10-173-226.eu-west-2.compute.amazonaws.com/job/Jenkins_c/env.BUILD_NUMBER/console\"}"
                     """
             } 
             }
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
}

