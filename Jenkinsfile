pipeline {
    agent any
     tools {
        maven 'maven3'
    }
    stages{
        stage('Build'){
            steps{
                
                def mvnHome = tool name: 'maven3', type: 'maven'
                sh "${mvnHome}/bin/mvn package"
            }
        }
    }
}
