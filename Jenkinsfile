node{
		stage('SCM'){
		git 'https://github.com/diaconovi/GitHelloWorld.git'
		}	
		stage('SonarQubeScan'){
			def scannerHone=tool 'SonarQube Scanner'
			WithSonarQubeEnv('localhost:9000'){
				sh './opt/sonar-scanner/bin/sonar-scanner'
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
