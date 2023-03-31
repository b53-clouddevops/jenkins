// An example of showing Declarative Pipeline
pipeline {
    agent any 

    environment { 
        ENV_URL  = "pipeline.learning.com"             // Declaring pipeline at Pipeline level
        SSH_CREDENTIALS = credentials('SSH_CRED') 
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
                sh "env"                                              // command which prints the existing environment variables
            }
        }

        stage('Stage Name - 3') {
            environment { 
                        ENV_URL = "stage.learning.com"               // Declaring pipeline at stage level
                }
            steps {
                sh '''
                    echo Printing the environment variable ${ENV_URL}
                
                '''
            }
        }
    }
}