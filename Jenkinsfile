pipeline {
    agent any
     environment { 
        ArtifactId= readMavenPom().getArtifactId() 
        GroupId = readMavenPom().getGroupId() 
        Version = readMavenPom().getVersion()
        Name =  readMavenPom().getName()
    }
    tools {
        maven 'maven'
    }
    stages {
        stage('Build stage') {
            steps {
                echo 'Building stage...'
                sh 'mvn clean install package'
            }
        }
        stage('Test stage') {
            steps {
                echo 'Testing stage...'
            }
        }
        stage('Upload to Nexus stage') {
            steps {
                echo 'Uploading stage...'
                script {
                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "SVVDevOps-SNAPSHOT" : "SVVDevOps-RELEASE"
                    nexusArtifactUploader artifacts: [
                    [
                        artifactId: "${ArtifactId}", 
                        classifier: '', 
                        file: "target/${ArtifactId}-${Version}.war", 
                        type: 'war'
                        ]
                    ], 
                        credentialsId: 'f96dfd41-08eb-4924-a2dd-92e56c19e853', 
                        groupId: "${GrpupID}", 
                        nexusUrl: '3.16.148.138:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: "${NexusRepo}", 
                        version: "${Version}"
            }
                }
        }
        stage('Deployment stage') {
            steps {
                echo 'Deploing stage...'
            }
        }
    }
}