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
                    nexusArtifactUploader artifacts: [[artifactId: '${POM_ARTIFACTID}', classifier: '', file: 'my-app/target/${POM_ARTIFACTID}-${POM_VERSION}.${POM_PACKAGING}', type: '${POM_PACKAGING}']], credentialsId: 'NEXUS_CRED', groupId: '${POM_GROUPID}', nexusUrl: '192.168.50.27:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '${POM_VERSION}'
                }
            }
        }
    }
    
}
