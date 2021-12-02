pipeline{
    agent any

    stages {

        stage('Get Source'){
            steps{
                git url: 'https://github.com/AlessandroMelo06/pedelogo-catalogo.git', branch: 'main'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dockerapp = docker.build("AlessandroMelo06/pedelogo-catalogo:${env.BUILD_ID}",
                        '-f ./src/PedeLogo.Catalogo.Api/Dockerfile .')
                }
            }
        }

        stage('Docker Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD+ID}")
                }
            }
        }
    }
}