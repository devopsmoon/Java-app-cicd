pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('git checkout'){
            steps{
                git url:'https://github.com/devopsmoon/Java-app-cicd.git',branch:'main'
            }
        }
    }
}