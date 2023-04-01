pipeline {
    agent any 
    stages {
        stage('checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/citrix2devops/war-web-project.git']])
                
            }
        }
        stage('package'){
            when {
                branch 'release'
            steps{
                sh 'mvn package'
            }
        }
    }
}
