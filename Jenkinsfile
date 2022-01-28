  pipeline {
    agent any
      environment {
        NEXUS_CREDS = credentials('NexusArtifactoryLogin')
        NEXUS_USER = "admin"
        NEXUS_PASSWORD = "admin"
    tools {
        maven 'maven3'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stages {
            stage('Nexus Deploy') {
                steps {
                    configFileProvider([configFile(fileId: 'maven-settings', variable: 'MAVEN_GLOBAL_SETTINGS')]) {
                        sh 'mvn -gs $MAVEN_GLOBAL_SETTINGS deploy'
                    }
                }
            }
        }
    }
}
