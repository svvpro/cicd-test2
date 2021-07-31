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
                        credentialsId: '799774dc-0070-407c-8099-39790234bd10', 
                        groupId: "${GroupID}", 
                        nexusUrl: '18.188.94.176:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: "${NexusRepo}", 
                        version: "${Version}"
            }
                }
        }
        stage ('Deploy to Tomcat'){
            steps {
                echo "Deploying ...."
                sshPublisher(publishers: 
                [sshPublisherDesc(
                    configName: 'Ansible_Controller', 
                    transfers: [
                        sshTransfer(
                                cleanRemote:false,
                                execCommand: 'ansible-playbook /home/ansibleadmin/download-and-deploy-tomcat.yaml -i /home/ansibleadmin/hosts',
                                execTimeout: 120000
                        )
                    ], 
                    usePromotionTimestamp: false, 
                    useWorkspaceInPromotion: false, 
                    verbose: false)
                    ])
            
            }
        }
        stage ('Deploy to Dcoker'){
            steps {
                echo "Deploying ...."
                sshPublisher(publishers: 
                [sshPublisherDesc(
                    configName: 'Ansible_Controller', 
                    transfers: [
                        sshTransfer(
                                cleanRemote:false,
                                execCommand: 'ansible-playbook /home/ansibleadmin/download-and-deploy-docker.yaml -i /home/ansibleadmin/hosts',
                                execTimeout: 120000
                        )
                    ],
                    usePromotionTimestamp: false, 
                    verbose: false)
                    ])
            
            }
        }
    }
}