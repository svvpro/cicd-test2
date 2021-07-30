pipeline {
    agent any
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
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'SVVDevOpsLab', 
                        classifier: '', 
                        file: 'target/SVVDevOpsLab-0.0.1-SNAPSHOT.war', 
                        type: 'war'
                        ]
                    ], 
                        credentialsId: 'f96dfd41-08eb-4924-a2dd-92e56c19e853', 
                        groupId: 'one.svv', 
                        nexusUrl: '3.16.148.138:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'SVVDevOps-SNAPSHOT', 
                        version: '0.0.1-SNAPSHOT'
            }
        }
        stage('Deployment stage') {
            steps {
                echo 'Deploing stage...'
            }
        }
    }
}