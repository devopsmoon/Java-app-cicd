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
  }
}