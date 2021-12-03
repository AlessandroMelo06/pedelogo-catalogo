pipeline {
agent any
stages {
    stage('Initialize'){
        steps {
                def dockerHome = tool 'myDocker'
                env.PATH = "${dockerHome}/bin:${env.PATH}"                }
        }
    stage('Push to Docker Registry'){
        steps {
            withCredentials([usernamePassword(credentialsId: 'dockerHubAccount', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {                
            pushToImage(CONTAINER_NAME, CONTAINER_TAG, USERNAME, PASSWORD)
            }            
        }  
    }
}}