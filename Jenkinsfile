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
			stage(${params.TestingType}) {
            steps {
                bat 'mvn clean install -DPROFILE=${params.TestingType}'
            }
        }
        
    }
}