pipeline {
    stages {
	    stage('SCM CHeckout') {
            steps {
               git https://github.com/lakshmipathi1997/ArexdataDemo
            }
        }
        stage('CheckMavenVersion') {
            steps {
                bat 'mvn --version'
            }
        }
         stage('Clean') {
            steps {
                bat 'mvn clean'
            }
			stage('SmokeTest') {
            steps {
                bat 'mvn clean install -DPROFILE=SmokeTest'
            }
        }
        }
    }
}