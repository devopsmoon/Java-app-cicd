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
    }
}