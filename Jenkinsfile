@Library('jenkins-shared-library') _
properties([
  parameters([
     string(name: 'appVersion', defaultValue: ''), //nodejseks pipeline is sending appversion and deploy to. we have to receive them.
     string(name: 'deploy_to', defaultValue: 'dev')
     ])
    ])

def configMap = [
    project: "roboshop",
    component: "catalogue",
    appVersion: (params.appVersion),
    deploy_to: (params.deploy_to)
]  

EKSDeploy(configMap) //after build we have to call eks deploy. send this configmap.