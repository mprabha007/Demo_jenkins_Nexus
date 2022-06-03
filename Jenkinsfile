pipeline {
    agent any
     tools {
        maven 'maven3'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                
                //def mvnHome = tool name: 'maven3', type: 'maven'
                //sh "${mvnHome}/bin/mvn package"
                sh script: 'mvn clean package'
            }
        }
        stage('Nexus_Push'){
            steps{
                script{
                def mavenPom = readMavenPom file : 'pom.xml'
                def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "Demo_Jenkins_nexus_snapshot" : "Demo_Jenkins_nexus"
              nexusArtifactUploader artifacts: 
                [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: "target/simple-app-${mavenPom.version}.war", 
                        type: 'war'
                    ]
                ], 
                credentialsId: 'Nexus', 
                groupId: 'in.javahome', 
                nexusUrl: '172.31.5.83:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: nexusRepoName,
                version: "${mavenPom.version}"
                }
            }
        }
    }
}
