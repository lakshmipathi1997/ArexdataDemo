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
	    
	     post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }

    }
}
