pipeline 
{
    agent any
    
    stages
    {
        stage('git checkout')
        {
            steps
            {
                git branch: 'chetan', url: 'https://github.com/Omega525/DevOps-chetan.git'

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