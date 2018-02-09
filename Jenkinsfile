pipeline{
	agent any
	stages{
		stage('GitHub'){
			steps{
				git 'https://github.com/diaconovi/GitHelloWorld.git'
			}
		}
		stage('SonarScanner'){
			steps{
				script{
				def scannerHome = tool 'SonarScanner'
				}
				withSonarQubeEnv('SonarQube Server'){
					sh "${scannerHome}/bin/sonar-scanner"
				}
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
