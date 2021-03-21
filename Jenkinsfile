pipeline {
    agent any
    options {
    buildDiscarder(logRotator(numToKeepStr:'1'))
    disableConcurrentBuilds()
    }
    stages {
        stage('checkout') {
            steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kliakos/sparkjava-war-example.git']]])
            }
        }
       stage('build') {
            steps {
            sh 'mvn clean package'
            }
        }
        stage('upload') {
            steps {
            nexusArtifactUploader artifacts: [[artifactId: 'ram', classifier: '', file: 'target/sparkjava-hello-world-1.0.war', type: 'war']], credentialsId: 'nexus', groupId: 'ram', nexusUrl: '18.188.25.100:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'java', version: '$BUILD_NUMBER'
            }
        }
    }
}
