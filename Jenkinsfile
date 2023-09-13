pipeline{
    agent any

  tools{
    maven 'maven'
  }
  stages{
    stage('Git Checkout'){
        steps{
            git branch: 'main', credentialsId: 'Jenkins', url: 'git@github.com:devopsmoon/Java-app-cicd.git'
        }
    }
    stage('Build'){
        steps{
            sh 'mvn clean package'
        }
    }
    stage('Sonar Analysis'){
        steps{
            withSonarQubeEnv(installationName: 'Sonar-Server', credentialsId: 'sonar'){
                sh 'mvn sonar:sonar'

            }
            
        }
    }
    stage('Nexus Push'){
        steps{
            nexusArtifactUploader artifacts: [
[
artifactId: 'hiring', 
classifier: '', 
file: 'target/hiring.war', 
type: 'war'
]
], 
credentialsId: 'nexus-user', 
groupId: 'in.javahome', 
nexusUrl: '10.0.0.109:8081/', 
nexusVersion: 'nexus3', 
protocol: 'http', 
repository: 'Java-App-Repo/', 
version: '0.1'
        }
    }
    stage('Deploy to servers'){
        steps{
            sshagent(['ubuntu-user']){
                sh """
                ssh -o StrictHostKeyChecking=no ubuntu@10.0.0.228 ls -lart
                scp -o StrictHostKeyChecking=no target/*.war ubuntu@10.0.0.228:/opt/tomcat9/webapps
                ssh -o StrictHostKeyChecking=no ubuntu@10.0.0.228 /opt/tomcat9/bin/shutdown.sh
                ssh -o StrictHostKeyChecking=no ubuntu@10.0.0.228 /opt/tomcat9/bin/startup.sh
                """
            }

        }
    }
  }
}