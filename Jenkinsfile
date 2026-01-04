pipeline {
    // This is a pre build section
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        COURSE = "Jenkins"
        appVersion = ""
        ACC_ID = "485658242739"
        PROJECT = "roboshop"
        COMPONENT = "catalogue"
        REGION = "us-east-1"
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }

   parameters {
       string(name: 'appVersion', description: 'Which app version you want to deploy')
       choice(name: 'deploy_to', choices: ['dev', 'qa', 'prod'], description: 'Pick something')
   
     }

    // This is a build section.
    stages {
        stage('Deploy') {
            steps {
                script { 
                    withAWS(region:'us-east-1',credentials:'aws-creds') {

                     sh """
                        aws eks update-kubeconfig --region ${REGION} --name ${PROJECT}-${params.deploy_to}
                     """
                }
                }

            }
        }

    }

    post {
        always {
            echo 'I will always say hello again!'
            cleanWs()
        }

        success {
            echo 'I will run if success'
        }
       
       failure {
           echo 'I will run if failure'
       }
       aborted {
            echo 'pipeline is aborted'
       }
    }
}