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
}
