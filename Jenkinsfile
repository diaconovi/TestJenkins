pipeline{
	agent any
	environment{
		def qg = waitForQualityGate()
	}
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
			steps{
				timeout(time: 2, unit: 'MINUTES') {
					script{
						whitSonarQubeEnv('SonarQube Server'){
							if (qg.status != 'OK') {
								error "Pipeline Aborted failure: ${qg.status}"
							}else {
								echo "Quality gate says: OK"
							}
							
						}
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
