pipeline {
agent any
stages {
    stage('Initialize'){
        steps {
                def dockerHome = tool 'myDocker'
                env.PATH = "${dockerHome}/bin:${env.PATH}"
        }
    }
}}