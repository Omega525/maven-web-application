pipeline 
{
    agent any
    
    stages
    {
        stage('git checkout')
        {
            steps
            {
                git branch: 'chetan', url: 'https://github.com/Omega525/maven-web-application.git'
            }
        }

        stage('build project')
        {
            steps
            {
                sh 'mvn clean install'
            }
        }
    }
}
