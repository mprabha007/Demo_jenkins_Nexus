pipeline {
    agent any
     tools {
        maven 'maven3'
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
            script{
                steps{
                    def mavenPom = readMavenPom file 'pom.xml'
                    nexusArtifactUploader artifacts: 
                        [
                            [
                                 artifactId: 'simple-app', 
                                 classifier: '', 
                                 file: "target/simple-app-${mavenPom}.war", 
                                 type: 'war'
                            ]
                        ], 
                        credentialsId: 'Nexus', 
                        groupId: 'in.javahome', 
                        nexusUrl: '172.31.5.83', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'Demo_Jenkins_nexus', 
                        version: "${mavenPom}"
                    }
                 }     
             }
        }
    }
}
