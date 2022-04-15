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
        stage('Gmail')
				{
					steps
					{
						emailext body: "*${currentBuild.currentResult}:* Job Name: ${env.JOB_NAME} || Build Number: ${env.BUILD_NUMBER}\n More information at: ${env.BUILD_URL}",
						subject: 'Test Automation Pipeline Build Status',
						to: 'lakshmipathimunna@gmail.com'
					}
				}
    }
}
