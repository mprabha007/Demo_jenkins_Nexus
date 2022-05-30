pipeline {
    agent any
    tool name: 'maven3', type: 'maven'
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
        }
    }
}
