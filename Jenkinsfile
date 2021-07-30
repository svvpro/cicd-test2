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
        stage('Deployment stage') {
            steps {
                echo 'Deploing stage...'
            }
        }
    }
}