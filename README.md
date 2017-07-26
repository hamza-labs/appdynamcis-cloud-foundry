### Monitor your cloud foundry application using appDynamics:

- This markdown shows you how to integrate AppDynamics with Cloud Foundry (Stackato, Community or Pivotal)

### Connect to Cloud FOundry using the CF CLI

`cf login -a https://api.cf.xxxx.xx -u username -p ********** -o your_app -s dev`

### create a file credentials.json with the following content

        {  
        "application-name":"your_app_name",
        "port":"443",
        "tier-name":"tier1",
        "node-name":"your_app_Tier",
        "account-access-key":"**********",
        "account-name":"****",
        "host-name":"****",
        "ssl-enabled":"true"
        }
        
### Create app-dynamics user provided service

`cf create-user-provided-service agent-app-dynamics -p credentials.json`

### Change the manifest.yml to bind the service (this action should be done before the cf push !!!!!:)

here is an example of the manifest.yml

        applications:
        - name: your_app
          memory: 1024M
          disk_quota: 1024M
          host: your_host
          path : target/your_app.war
          services :
           - agent-app-dynamics

### Push your application to Cloud Foundry
`cf push`

### Connect to your application and generate some monitoring data
`https://your_app.io`

### Connect to appDynamics dashboard to see the result
`https://your_appdynamics_host.com`

