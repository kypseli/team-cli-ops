node('master') {
    echo "preparing Jenkins CLI"
    sh 'curl -O http://cjoc/cjoc/jnlpJars/jenkins-cli.jar'
    withCredentials([string(credentialsId: 'beedemo-admin-jenkins-api-key', variable: 'API_KEY')]) {
        sh """
          alias cli='java -jar jenkins-cli.jar -s \'http://cjoc/cjoc/\' -auth beedemo-admin:$API_KEY'
          cli help
        """
    }
}
