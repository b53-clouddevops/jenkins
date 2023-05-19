// // An example of showing Declarative Pipeline
pipeline {
    agent { label 'ws' }

    environment { 
        ENV_URL  = "pipeline.learning.com"             // Declaring pipeline at Pipeline level
        SSH_CREDENTIALS = credentials('SSH_CRED') 
    }

    // triggers { pollSCM('*/1 * * * *') }

    // parameters {
    //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    // }

    stages {

        stage('Example on parallel stages') {
            parallel {
                stage('One') {
                    steps {
                    script {
                        env.MYSECRET=sh(returnStdout: true, script: "aws secretsmanager get-secret-value --secret-id roboshop/secrets  --region us-east-1  | jq --raw-output '.SecretString' | jq -r '.SSH_PASSWORD'").trim()
                        }
                        sh "aws secretsmanager get-secret-value --secret-id roboshop/secrets  --region us-east-1  | jq --raw-output '.SecretString' | jq -r '.SSH_PASSWORD'"
                        sh "cat /home/centos/secret.txt"
                        sh "echo Printing the secret ${MYSECRET}"
                    }
                }
                stage('Two') {
                    steps {
                        sh "echo STAGE TWO"
                        sh "sleep 1"
                        sh "echo Printing ${MYSECRET}"
                    }
                }
                stage('Three') {
                    steps {
                        sh "echo STAGE THREE"
                        sh "sleep 1"
                    }
                }
            }
        }
            
        stage('Stage Name - 1') {
            steps {
                sh "echo I am using the Pipeline Syntax Help"
            }
        }

        stage('Stage Name - 2') {
            when { branch 'dev' }
            steps {
                sh "echo Printing the environment variable ${ENV_URL}"
                sh "env"                                              // command which prints the existing environment variables
            }
        }
    }
}


// node {
//     stage('Test') {
//         print 'Welcome to scripted pipelines'
//     }
//     stage('QA') {
//         print 'Scripted pipelines makes things easy and DRY'
//     }
// }