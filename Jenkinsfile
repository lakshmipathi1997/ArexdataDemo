pipeline {
    agent any
    stages {
        stage('No-op') {
            steps {
                bat 'dir'
            }
        }
    }
    post {
        always {
            echo 'One way or another, I have finished'
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
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
}
