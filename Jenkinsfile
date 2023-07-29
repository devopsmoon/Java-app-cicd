pipeline{
    agent any
    tools{
        maven 'M2_HOME'
        java  'openjdk'
    }
    stages{
        stage('git checkout'){
            steps{
                git url:'https://github.com/devopsmoon/Java-app-cicd.git',branch:'main'
            }
        }
    }
}