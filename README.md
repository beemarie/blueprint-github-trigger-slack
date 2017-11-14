## Blueprint that does the equivalent of the following:

  *  `wsk -i package bind /whisk.system/github openwhisk-github --param username <username> --param repository <repositoryName> --param accessToken <githubAccessToken>`  
  * `wsk -i trigger create github-trigger --feed openwhisk-github/webhook --param events push`  
  * `wsk -i action create message-ify-github-response`  
  * `wsk -i rule create connect-github-trigger-to-slack-action github-trigger message-ify-github-response`  
  * `wsk package bind /whisk.system/slack openwhisk-slack --param channel "#<channelName>" --param url "<slackApiWebhook>"  --param username "<username>"`
  * `wsk action create github_slack_integration_sequence --sequence message-ify-github-response,openwhisk-slack/post`
  * `wsk -i rule update connect-github-trigger-to-slack-action github-trigger github_slack_integration_sequence`

## Running the Trigger / Actions
  * `git clone <githubRepositoryCloneURI>`
  * `cd <repositoryName>`
  * `touch test.js`
  * `git add test.js`
  * `git commit -m "testing"`
  * `git push origin master`

## Troubleshooting  
  * Go to the git repository that you bound the openwhisk-github package to.
  * Click on settings
  * Click on webhooks
  * See if the event is being sent to the correct location
