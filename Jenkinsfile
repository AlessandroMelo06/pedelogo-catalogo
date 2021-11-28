pipeline{
    agent any

    stages {

        stage('Get Source')
            steps{
                git url: 'https://github.com/AlessandroMelo06/pedelogo-catalogo.git', branch: 'main'
            }

        }
        stage('Docker Build') {
            steps {
                scripts {
                    dockerapp = docker.build("alessandromelo06/pedelogocatalogo:${env.BUILD_ID}",
                        '-f src/PedeLogo.Catalogo.Api/Dockerfile .')
                }
                
            }
        }
        
        stage('Docker Push Imagem') {
            steps {
                scripts{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                    dockerapp.Push('latest')
                    dockerapp.Push("${env.BUILD_ID}")
               }

            }
        }
    }
}