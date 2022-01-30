pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
        }    
    }
    stage('Nexus Deploy') {
        steps {
            configFileProvider([configFile(fileId: 'maven-settings', variable: 'MAVEN_GLOBAL_SETTINGS')]) {
                sh 'mvn -gs $MAVEN_GLOBAL_SETTINGS deploy'
            }
        }
    }
}
