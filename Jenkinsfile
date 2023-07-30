pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Check'){
            steps{
                git url:'https://github.com/devopsmoon/Java-app-cicd.git',branch:'main'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Sonarqube-Analysis'){
            steps{
                withSonarQubeEnv(installationName: 'sonarqube8', credentialsId: 'sonar'){
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
file: 'target/hiring.war', 
type: 'war'
]
], 
credentialsId: 'nexus_cred', 
groupId: 'in.javahome', 
nexusUrl: '44.201.131.231:8081', 
nexusVersion: 'nexus3', 
protocol: 'http', 
repository: 'Java-App/', 
version: '0.1'
            }
        }
        stage('Deploy to Tomcat'){
            steps{
                sshagent(['ubuntu']) {
                    sh """
                    scp -o StrictHostKeyChecking=no target/*.war ubuntu@174.129.113.20:/opt/tomcat/webapps
                    ssh -o StrictHostKeyChecking=no ubuntu@174.129.113.20 stoptomcat
                    ssh -o StrictHostKeyChecking=no ubuntu@174.129.113.20 startomcat
                    """
                }

            }
        }
    }
}