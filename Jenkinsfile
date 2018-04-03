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
        sleep time: 2, unit: 'MINUTES'
        waitUntil {
          try {
            sh """
              alias cli='java -jar jenkins-cli.jar -s \'http://cjoc/cjoc/\' -auth beedemo-admin:$API_KEY'
              cli teams api | grep 'READY'
            """
            return true
          } catch (exception) {
            return false  
          }
        }
        echo 'successfully created api team'
        echo 'adding custom ops role'
        sh """
          alias cli='java -jar jenkins-cli.jar -s \'http://cjoc/cjoc/\' -auth beedemo-admin:$API_KEY'
          cli team-roles api --add TEAM_OPS --display 'Team Ops'
          cli team-permissions api TEAM_OPS --put < ops-permissions.json
          cli team-members api --add kypseli*ops --roles TEAM_OPS
        """
        echo 'finished setting up ops role for api team'
    }
}
