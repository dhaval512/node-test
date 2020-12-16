pipeline{
    agent any 
      environment {        
        SLACK_COLOR_DANGER  = '#E01563'
        SLACK_COLOR_INFO    = '#6ECADC'
        SLACK_COLOR_WARNING = '#FFC300'
        SLACK_COLOR_GOOD    = '#3EB991'
        JOB_NAME            = 'test'
        SLACK_CHANNEL       = 'ortholoop-devops'
   	
    }
    stages{
        stage('docker file for stage'){
            steps{
                sh '''
                echo "hello"
                '''
                 }
            }
        }
post {
        aborted {
            echo "Sending message to Slack"
            slackSend (color: "${env.SLACK_COLOR_WARNING}",
                       channel: "${env.SLACK_CHANNEL}",
                       message: "*ABORTED:* Pipeline: ${env.JOB_NAME} - #${env.BUILD_NUMBER} \n Application: ${env.APPLICATION_NAME} \n More info at: ${env.BUILD_URL}")
        } // aborted
        failure {
            echo "Sending message to Slack"
            slackSend (color: "${env.SLACK_COLOR_DANGER}",
                       channel: "${env.SLACK_CHANNEL}",
                       message: "*FAILED:* Pipeline: ${env.JOB_NAME} - #${env.BUILD_NUMBER} \n Application: ${env.APPLICATION_NAME} \n More info at: ${env.BUILD_URL}")
        } // failure
        success {
            echo "Sending message to Slack"
            slackSend (color: "${env.SLACK_COLOR_GOOD}",
                       channel: "${env.SLACK_CHANNEL}",
                       message: "*SUCCESS:* Pipeline: ${env.JOB_NAME} - #${env.BUILD_NUMBER} \n Application: ${env.APPLICATION_NAME} \n More info at: ${env.BUILD_URL}")
        } // success
    } // post 	
}
