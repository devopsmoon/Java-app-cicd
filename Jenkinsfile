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
                withSonarQubeEnv(installationName: 'sonarqube8', credentialsId: 'sonar')
                sh 'mvn sonar:sonar'
            }
        }
    }
}