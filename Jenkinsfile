pipeline {
  agent { label 'master' }
  
  stages {
    stage('create teams') {
      steps {
        echo ""
        sh 'curl -O http://cjoc/cjoc/jnlpJars/jenkins-cli.jar'
        sh 'java -jar jenkins-cli.jar -s http://cjoc/cjoc/ help'
      }
    }
  }
}
