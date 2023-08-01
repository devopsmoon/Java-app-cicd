pipeline{
    agent any
    tools {
        maven 'maven'
    }
    options {
    buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
  }
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', credentialsId: 'Jenkins-user', url: 'git@github.com:devopsmoon/Java-app-cicd.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Sonarqube Analysis'){
            steps{
                withSonarQubeEnv(installationName: 'sonarqube',credentialsId: 'Sonar-Token'){
                sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Nexus Pull'){
            steps{
            nexusArtifactUploader artifacts: [
[
artifactId: 'hiring', 
classifier: '',
file: 'target/hiring.war', type: 'war'
]
], 
credentialsId: 'Nexus-User', 
groupId: 'in.javahome', 
nexusUrl: '3.93.10.183:8081/', 
nexusVersion: 'nexus3', 
protocol: 'http', 
repository: 'Java-App/', 
version: '4.0.0'
            }
        }
        stage('Deploy To Server'){
            steps{
                sshagent(['ubuntu']){
                sh """
                scp -o StrictHostKeyChecking=no target/*.war ubuntu@34.238.50.219:/opt/tomcat/webapps/
                ssh -o StrictHostKeyChecking=no ubuntu@34.238.50.219 stoptomcat
                ssh -o StrictHostKeyChecking=no ubuntu@34.238.50.219 startomcat
                """
                }
                
            }
        }
    }
}