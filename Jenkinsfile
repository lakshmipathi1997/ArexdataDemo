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
    }
    post {
        always {
            echo 'checking Maven Version again'
			   bat 'mvn --version'
			   echo 'Maven version has been Verified'
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            slackUploadFile channel: 'arexdataautomationreports', credentialId: 'Pq9ZMt7CZvXq49LmoNJEHUG8', filePath: '"C:\\Users\\Dell\\ArexdataAutomation\\qa-automation\\test-output"', initialComment: 'AutomationTestReport'
        }
        changed {
            echo 'Things were different before...'
        }
    }
}  
