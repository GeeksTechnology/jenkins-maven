pipeline {

    agent any

    tools {

        maven "MAVEN"
    }

    
    stages {
        stage('Build Maven') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GIT_REPO', url: 'https://github.com/devopshint/jenkins-maven.git']]])

                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
            }
        }
        stage('Push to Artefact'){

            steps{
                script{
                    nexusArtifactUploader artifacts: [[artifactId: 'pom.my-app', classifier: '', file: 'pom.xml', type: 'pom']], credentialsId: 'NEXUS_CRED', groupId: 'pom.com.mycompany.app', nexusUrl: '192.168.50.27:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-central-repository', version: 'pom.1.0-SNAPSHOT'
                }
            }
        }
    }
    
}
