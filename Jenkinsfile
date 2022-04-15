pipeline {
    stages {
        stage('Clean') {
            steps {
                echo 'Hello World'
                bat "mvn --version"
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
    }
}