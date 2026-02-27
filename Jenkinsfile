pipeline 
{
    agent any
   

    environment
    {
        buildNumber = "${env.BUILD_NUMBER}"
    }
    
    stages
    {
        stage('git checkout')
        {
            steps
            {
                git branch: 'main', url: 'https://github.com/Omega525/maven-web-application.git'
            }
        }

        stage('build project')
        {
            steps
            {
                sh 'mvn clean install'
            }
        }
    stage(build docker image)
        {
            steps
            {
                sh 'sudo docker build -t ch3tan525/maven-web-application:${buildNumber} .'
            }
        }
    stage('push docker image')
        {
            steps
            {
                withCredentials([string(credentialsId: 'docker_hub_pass', variable: 'docker_pass')])
                 {
                    sh 'sudo docker login -u ch3tan525 -p ${docker_pass}'
                }
                    sh 'sudo docker push ch3tan525/maven-web-application:${buildNumber}'

    stage( 'remove docker image')
        {
            steps
            {
                sh 'docker rmi ch3tan525/maven-web-application:${buildNumber}'
            }
        }
             }
        }
    }
}
