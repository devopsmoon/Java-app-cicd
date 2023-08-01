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
    }
}