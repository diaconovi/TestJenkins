node {
  stage('SCM') {
    git 'https://github.com/diaconovi/GitHelloWorld.git'

  }
  stage('SonarQube analysis') {
    // requires SonarQube Scanner 2.8+
    def scannerHome = tool 'SonarScanner';
    withSonarQubeEnv('SonarQube Server') {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
stage("Quality Gate"){
	sh sleep 10
  timeout(time: 1, unit: 'MINUTES') { // Just in case something goes wrong, pipeline will be killed after a timeout
    def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
    if (qg.status != 'OK') {
      error "Pipeline aborted due to quality gate failure: ${qg.status}"
    }
  }
}

