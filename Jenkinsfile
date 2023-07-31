pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('checkout'){
            steps{
                git branch: 'main', credentialsId: 'Jenkins-ssh', url: 'git@github.com:devopsmoon/Java-app-cicd.git'
            }
            
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Sonarqube Analysis'){
            steps{
                withSonarQubeEnv(credentialsId: 'sonarqube'){
                sh 'mvn sonar:sonar'
                }
                
            }
        }
        stage(('Nexus Push')){
            steps{
            nexusArtifactUploader artifacts: [
[
artifactId: 'hiring', 
classifier: '', 
file: 'target/hiring.war', 
type: 'war'
]
],
credentialsId: 'nexus-cred',
groupId: 'in.javahome', 
nexusUrl: '52.87.205.138:8081', 
nexusVersion: 'nexus3',
protocol: 'http', 
repository: 'Java-App/', 
version: '4.0.0'
            }
        }
        stage('deploy to tomcat server'){
            steps{
                sshagent(['tomcat']){
                    sh """
                    ssh -o StrictHostkeyChecking=no ls -lart
                    scp -o StrictHostKeyChecking=no target/hiring.war tomcat@3.95.199.9:/opt/tomcat-9/webapps/
                    ssh -o StrictHostkeyChecking=no tomcat@3.95.199.9 stoptomcat
                    ssh -o StrictHostKeyChecking=no tomcat@3.95.199.9 startomcat
                    """
                }
            }
        }
    }
}