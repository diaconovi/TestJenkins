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
				scannerHome = tool 'SonarScanner'
				}
				withSonarQubeEnv('SonarQube Server'){
					sh "${scannerHome}/bin/sonar-scanner"
				}
			}
		}
		stage('Quality Gate'){
			timeout(time: 2, unit: 'MINUTES'){
				script{
				def qg = waitForQualityGate()
				if qg =! 'OK'{
					error "Pipeline Aborted failure: ${qg.status}"
					}
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
