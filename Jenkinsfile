// An example of showing Declarative Pipeline
pipeline {
    agent any 

    environment { 
        ENV_URL  = "pipeline.learning.com"             // Declaring pipeline at Pipeline level
        SSH_CREDENTIALS = credentials('SSH_CRED') 
    }

    triggers { pollSCM('*/1 * * * *') }

    // parameters {
    //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    // }

    stages {
    
        stage('Testing mvn commands') {
            steps {
                sh "mvn clean"
            }
        }
       
        stage('Stage Name - 1') {
            steps {
                sh "echo I am using the Pipeline Syntax Help"
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