node('master') {
    properties([parameters([string(defaultValue: '', description: 'Name of team to create with associated named json file.', name: 'teamName', trim: false)])])
    if(params.teamName) {
        echo "preparing to create ${params.teamName} team"
        checkout scm
        echo "preparing Jenkins CLI"
        sh 'curl -O http://cjoc/cjoc/jnlpJars/jenkins-cli.jar'
        withCredentials([string(credentialsId: 'beedemo-ops-jenkins-api-key', variable: 'API_KEY')]) {
            //check if team is already created or not
            def createTeam
            try {
                sh """
                  alias cli='java -jar jenkins-cli.jar -s \'http://cjoc/cjoc/\' -auth beedemo-ops:$API_KEY'
                  cli teams ${params.teamName} | grep 'READY'
                """
                createTeam = false
            } catch (exception) {
                createTeam = true  
            }
            if(createTeam) {
                //recipes are updated every run
                sh """
                  alias cli='java -jar jenkins-cli.jar -s \'http://cjoc/cjoc/\' -auth beedemo-ops:$API_KEY'
                  echo 'creating team recipes'
                  cli team-creation-recipes --put < team-recipes.json
                  echo 'creating ${params.teamName} team'
                  cli teams ${params.teamName} --put < ${params.teamName}-team.json
                """
                //takes at least 2 minutes, so no need to check completion right away
                sleep time: 2, unit: 'MINUTES'
                waitUntil {
                  //wait until team is ready before adding additional role and member(s)
                  try {
                    sh """
                      alias cli='java -jar jenkins-cli.jar -s \'http://cjoc/cjoc/\' -auth beedemo-ops:$API_KEY'
                      cli teams ${params.teamName} | grep 'READY'
                    """
                    return true
                  } catch (exception) {
                    return false  
                  }
                }
                echo "successfully created ${params.teamName} team"
                echo 'adding custom ops role'
                sh """
                  alias cli='java -jar jenkins-cli.jar -s \'http://cjoc/cjoc/\' -auth beedemo-ops:$API_KEY'
                  cli team-roles ${params.teamName} --add TEAM_OPS --display 'Team Ops'
                  cli team-permissions ${params.teamName} TEAM_OPS --put < ops-permissions.json
                  cli team-members ${params.teamName} --add kypseli*ops --roles TEAM_OPS
                """
                echo "finished setting up ops role for ${params.teamName} team"
            }
            else {
                echo "${params.teamName} team was already created"
            }
        }
    }
}
