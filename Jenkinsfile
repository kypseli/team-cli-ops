pipeline {
  agent kubernetes
  
  stages {
    stage('create teams') {
      steps {
        sh 'JENKINS_CLI create team'
      }
    }
  }
}
