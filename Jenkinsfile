pipeline {
    agent any
    stages {
                stage('CheckMavenVersion') {
            steps {
                bat 'mvn --version'
            }
        }
	    stage('SendSlackNotification') {
            steps {
	       slackSend channel: 'arexdataautomationreports', message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}"
               slackSend channel: 'arexdataautomationreports ', message: 'Build Has been started'
	       slackSend color: "#439FE0", message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}"
            }
        }
         stage('Clean') {
            steps {
                bat 'mvn clean'
            }
			}
			stage('Tests') {
            steps {
                bat 'mvn clean install -P %TestingType%'
            }
        } 
	  stage('Gmail Notification')
				{
					steps
					{
						emailext attachmentsPattern: '**/report.html', body: 'Find attachments', subject: 'Arexdata_AutomationBuild_Report, to: 'lakshmipathi.kantipalli57@gmail.com'
						mail bcc: '', body: '''Hi , Here are your Build Results ,Please Find
                                                Thanks
                                                Lakshmipathi''', cc: 'siva0750@gmail.com', from: '', replyTo: '', subject: 'Arexdata Jenkins Build Results', to: 'lakshmipathi.kantipalli57@gmail.com'
					}
				}  
    }
    post {
        always {
            echo 'checking Maven Version again'
			   bat 'mvn --version'
			   echo 'Maven version has been Verified'
		           slackUploadFile channel: 'arexdataautomationreports', credentialId: 'Pq9ZMt7CZvXq49LmoNJEHUG8', filePath:"index.html", initialComment: 'AutomationTestReport'
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            slackUploadFile channel: 'arexdataautomationreports', credentialId: 'Pq9ZMt7CZvXq49LmoNJEHUG8', filePath: '"C:/Users/Dell/.jenkins/workspace/ArexdataTest/test-output/selenium-automation-report.html"', initialComment: 'AutomationTestReport'
        }
        changed {
            echo 'Things were different before...'
	    slackUploadFile channel: 'arexdataautomationreports', credentialId: 'Pq9ZMt7CZvXq49LmoNJEHUG8', filePath: '"C:/Users/Dell/.jenkins/workspace/ArexdataTest/test-output/selenium-automation-report.html"', initialComment: 'AutomationTestReport'
        }
    }
}  
