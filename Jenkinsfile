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
        stage('Docker Push Image') {
            steps {
                script {
                    docker run --rm -u root -p 8081:30001 -v jenkins-data:/var/jenkins_home -v $(which docker):/usr/bin/docker -v /var/run/docker.sock:/var/run/docker.sock -v "$HOME":/home jenkinsci/blueocean
                }
            }
        }
    }
}