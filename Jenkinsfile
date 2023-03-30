// An example of showing Declarative Pipeline
pipeline {
    agent any 
    stages {

        stage('Stage Name - 1') {
            steps {
                sh "echo I am using Pipeline Syntax Help"
            }
        }

        stage('Stage Name - 2') {
            steps {
                sh "echo I am executing stage - 2"
            }
        }

        stage('Stage Name - 3') {
            steps {
                sh '''
               
                echo I am using Pipeline Syntax Help
                echo demo to show multiple lines
                echo Printing multiple lines with a single usage of sh command
                
                '''
            }
        }

    }
}