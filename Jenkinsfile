pipeline 
{
    agent any
   
    tools
    {
        maven 'maven 3.9.9'
    }

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
    stage('build docker image')
        {
            steps
            {
                sh 'docker build -t ch3tan525/maven-web-application:${buildNumber} .'
            }
        }
    stage('push docker image')
        {
            steps
            {
                withCredentials([string(credentialsId: 'docker_hub_pass', variable: 'docker_pass')])
                 {
                    sh 'docker login -u ch3tan525 -p ${docker_pass}'
                }
                    sh  'docker push ch3tan525/maven-web-application:${buildNumber}'
                  
                    sh 'docker rmi ch3tan525/maven-web-application:${buildNumber}'

            }
        }

    stage('Deploy application to deployment server')
        {
            steps()
            {
               sshagent(['Deployment_server'])
               {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.45.222 "docker rm -f maven-container || true && docker run -d -p 8080:8080 --name maven-container ch3tan525/maven-web-application:${buildNumber}"'
                } 
            }
        }
    }
}
