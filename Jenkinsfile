pipeline{
    agent any

    stages {

        stage('Get Source'){
            steps{
                git url: 'https://github.com/alessandromelo06/pedelogo-catalogo.git', branch: 'main'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    dockerapp = docker.build("alessandromelo06/pedelogo-catalogo:${env.BUILD_ID}",
                        '-f ./src/PedeLogo.Catalogo.Api/Dockerfile .')
                }
            }
        }
        stage('Initialize'){
            def dockerHome = tool 'myDocker'
            env.PATH = "${dockerHome}/bin:${env.PATH}"
        }
        stage('Docker Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")
                }
            }
        }
    }
}