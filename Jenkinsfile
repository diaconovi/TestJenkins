pipeline {
    agent {
        docker { image 'maven:latest' 
                }    
            }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'successful'
        }
        failure {
            echo 'Failed'
        }
        unstable {
            echo 'Unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'this time was successful'
        }
    }
}
