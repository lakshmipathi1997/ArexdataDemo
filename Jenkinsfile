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
	       stage('GmailNotification'){
		    steps{
			emailext attachmentsPattern: '**/selenium-automation-report.html', body: 'Hi Team ,Please Find attachment for Passes TestCases', subject: 'AutomationTest', to: 'siva0750@gmail.com'    
		    }
	    }
    }
    post {
        always {
            echo 'checking Maven Version again'
			   bat 'mvn --version'
			   echo 'Maven version has been Verified'
		           slackUploadFile channel: 'arexdataautomationreports', credentialId: 'Pq9ZMt7CZvXq49LmoNJEHUG8', filePath:"**/selenium-automation-report.html", initialComment: 'AutomationTestReport'
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
	    emailext attachmentsPattern: '**/selenium-automation-report.html', from:'JenkinsAutomationReports@arexdata.com', body: 'Hi Team ,Please Find the Attachment For Failed Test Cases below', subject: 'AutomationTest', to: 'nakhter0441@gmail.com,lakshmipathi.kantipalli57@gmail.com'    
            slackUploadFile channel: 'arexdataautomationreports', credentialId: 'Pq9ZMt7CZvXq49LmoNJEHUG8', filePath: '"C:/Users/Dell/.jenkins/workspace/ArexdataTest/test-output/selenium-automation-report.html"', initialComment: 'AutomationTestReport'
		
        }
        changed {
            echo 'Things were different before...'
	    slackUploadFile channel: 'arexdataautomationreports', credentialId: 'Pq9ZMt7CZvXq49LmoNJEHUG8', filePath: '"C:/Users/Dell/.jenkins/workspace/ArexdataTest/test-output/selenium-automation-report.html"', initialComment: 'AutomationTestReport'
        }
    }
}  
