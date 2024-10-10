node('ubuntu-appserver-CWEB2140')
{
    def app
    stage('Cloning-Git')
    {
        // making sure we have the repository cloned to our workspace
        checkout scm
    }

    stage('Build-and-Tag')
    {
        // building the actual image
        app = docker.build('spcasagrande/car_docker_repo')
    }

    stage('Post-to-Dockerhub')
    {
        // posting the image
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
        {
            app.push('latest')
        }
    }

    stage('Deploy')
    {
        // deploying the application
        sh "docker-compose down"
        sh "docker-compose up -d"
    }
}
