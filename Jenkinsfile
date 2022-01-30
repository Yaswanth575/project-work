 pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{
                    configFileProvider(
                        [configFile(fileId: 'maven-settings', variable: 'MAVEN_GLOBAL_SETTINGS')]) {
                        sh 'mvn -s $MAVEN_GLOBAL_SETTINGS deploy'
                }
                    
            }
        }
    }
}
