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
                nexusArtifactUploader credentialsId: 'f235a4ee-4752-46b9-85e3-e39d31c020c2', 
                groupId: 'one.svv', 
                nexusUrl: '3.17.10.223:8081/', 
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