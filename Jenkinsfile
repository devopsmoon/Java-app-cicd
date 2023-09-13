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
  }
}