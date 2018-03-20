# team-cli-ops
CJE Team creation scripts

### create team recipes
`JENKISN_CLI team-creation-recipes --put < all-recipes.json`

### create API Team
`JENKISN_CLI teams api --put < api-team.json`
##### add ops role, ops permissions and ops members
`JENKISN_CLI team-roles api --add TEAM_OPS --display 'Team Ops'`

`JENKISN_CLI team-permissions api TEAM_OPS --put < ops-permissions.json `

`JENKISN_CLI team-members api --add kypseli*ops --roles TEAM_OPS`

### create UI Team
`JENKISN_CLI teams ui --put < ui-team.json`
##### add ops role, ops permissions and ops members
`JENKISN_CLI team-roles ui --add TEAM_OPS --display 'Team Ops'`

`JENKISN_CLI team-permissions ui TEAM_OPS --put < ops-permissions.json `

`JENKISN_CLI team-members ui --add kypseli*ops --roles TEAM_OPS`
