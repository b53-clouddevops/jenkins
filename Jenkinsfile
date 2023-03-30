// An example of showing Declarative Pipeline
pipeline {
    agent any 

    environment { 
        ENV_URL = "pipeline.learning.com"
    }

    stages {

        stage('Stage Name - 1') {
            steps {
                sh "echo I am using Pipeline Syntax Help"
            }
        }

        stage('Stage Name - 2') {
            steps {
                sh "echo Printing the environment variable ${ENV_URL}"
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