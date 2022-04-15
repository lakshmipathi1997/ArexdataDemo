pipeline {
     agent any
    stages {
        stage('CheckMavenVersion') {
            steps {
                bat 'mvn --version'
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

	    stage('SendExtentReports'){
		    steps{
			emailext attachmentsPattern: '**/report.html', body: 'Find attachments', subject: 'test', to: 'lakshmipathimunna@gmail.com'
		    }
	    }
	    post
	{
		always 
		{
            		echo 'This Job is Failed - Notifications have been sent to Gmail..!!'
			message: "*${currentBuild.currentResult}:* Job Name: ${env.JOB_NAME} || Build Number: ${env.BUILD_NUMBER}\n More information at: ${env.BUILD_URL}"
        		
			emailext body: "*${currentBuild.currentResult}:* Job Name: ${env.JOB_NAME} || Build Number: ${env.BUILD_NUMBER}\n More information at: ${env.BUILD_URL}",
			subject: 'Test Automation Pipeline Build Status',
			to: 'lakshmipathimunna@gmail.com'
		}
        	unstable 
		{
           		echo 'This Job is Unstable - Notifications have been sent to Gmail..!!'
			message: "*${currentBuild.currentResult}:* Job Name: ${env.JOB_NAME} || Build Number: ${env.BUILD_NUMBER}\n More information at: ${env.BUILD_URL}"
			emailext body: "*${currentBuild.currentResult}:* Job Name: ${env.JOB_NAME} || Build Number: ${env.BUILD_NUMBER}\n More information at: ${env.BUILD_URL}",
			subject: 'Test Automation Pipeline Build Status',
			to: 'lakshmipathimunna@gmail.com'
		}
	}
    }
}
