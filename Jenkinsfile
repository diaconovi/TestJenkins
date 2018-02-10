pipeline{
	agent any
	stages{
		stage('GitHub'){
			steps{
				git 'https://github.com/diaconovi/GitHelloWorld.git'
			}
		}
		
		stage('SonarQube Scan'){
			steps{
				script{
					ScannerHome = tool 'SonarScaner'
					withSonarQubeEnv('SonarQube Server'){
						sh "${scannerHome}/bin/sonar-scanner"
					}
				}
			}
		}
		
		stage('SonarQube Quality Gate'){
			steps{
				timeout(time: 2, unit: 'MINUTES'){
					script{
						withSonarQubeEnv{
				    		def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
    						if (qg.status != 'OK') {
      							error "Pipeline aborted due to quality gate failure: ${qg.status}"
    						}else{
    							echo "Quality Gate: ${qg.status}"
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
			echo 'This will run only if successful'
		}
		failure {
			echo 'This will run only if failed'
		}
		unstable {
			echo 'This will run only if the run was marked as unstable'
		}
		changed {
			echo 'This will run only if the state of the Pipeline has changed'
			echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}