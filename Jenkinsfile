pipeline {
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
			stage('SmokeTest') {
            steps {
                bat 'mvn clean install -DPROFILE=SmokeTest'
            }
        }
		
        }
    }
}