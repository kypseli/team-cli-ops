node('master') {
    echo "preparing Jenkins CLI"
    sh 'curl -O http://cjoc/cjoc/jnlpJars/jenkins-cli.jar'
    withCredentials([string(credentialsId: 'beedemo-admin-jenkins-api-key', variable: 'API_KEY')]) {
      //sh "CRUMB=$(curl -s 'http://cjoc/cjoc/crumbIssuer/api/xml?xpath=concat(//crumbRequestField,':',//crumb)' -u beedemo-admin:$API_KEY)"
      sh "java -jar jenkins-cli.jar -s http://cjoc/cjoc/ -u beedemo-admin:$API_KEY help"
    }
}
