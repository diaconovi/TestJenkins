node{
		stage('SCM'){
		git 'https://github.com/diaconovi/GitHelloWorld.git'
		}	
		stage('SonarQubeScan'){
			WithSonarQubeEnv('localhost:9000'){
				sh mvn sonar:sonar
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
