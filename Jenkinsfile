pipeline {
  agent { label 'master' }
  
  stages {
    stage('create teams') {
      steps {
        echo ""
        sh 'JENKINS_CLI create team'
      }
    }
  }
}
