node('master') {
    checkout scm
    echo "preparing Jenkins CLI"
    sh 'curl -O http://cjoc/cjoc/jnlpJars/jenkins-cli.jar'
    withCredentials([string(credentialsId: 'beedemo-admin-jenkins-api-key', variable: 'API_KEY')]) {
        sh """
          alias cli='java -jar jenkins-cli.jar -s \'http://cjoc/cjoc/\' -auth beedemo-admin:$API_KEY'
          echo 'creating team recipes'
          cli team-creation-recipes --put < team-recipes.json
          echo 'creating api team'
          cli teams api --put < api-team.json
        """
        
        waitUntil {
          sh """
            alias cli='java -jar jenkins-cli.jar -s \'http://cjoc/cjoc/\' -auth beedemo-admin:$API_KEY'
            cli teams api | grep 'success'
          """
        }
        echo 'successfully created api team'
    }
}
