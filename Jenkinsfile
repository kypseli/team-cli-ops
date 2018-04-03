node('master') {
  stage('create teams') {
    echo "preparing Jenkins CLI"
    sh 'curl -O http://cjoc/cjoc/jnlpJars/jenkins-cli.jar'
    sh 'java -jar jenkins-cli.jar -s http://cjoc/cjoc/ help'
  }
}
