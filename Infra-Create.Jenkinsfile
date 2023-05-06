pipeline {
    agent any 
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select The Environment')
    }
    options {
        ansiColor('xterm')    // Add's color to the output : Ensure you install AnsiColor Plugin.
    }
    stages {
        stage('Terraform Create Network') {
            steps {
                git branch: 'main', url: 'https://github.com/b53-clouddevops/terraform-vpc.git'
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                }
            }

        stage('Terraform Create ALB') {
            steps {
                git branch: 'main', url: 'https://github.com/b53-clouddevops/terraform-loadbalancers.git'
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                }
            }

        stage('Terraform Create Databases') {
            steps {
                        git branch: 'main', url: 'https://github.com/b53-clouddevops/terraform-databases.git'
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                    }
                }
        stage('Backend') {
            parallel {
                stage('Create Cart') {
                    steps {
                        git branch: 'main', url: 'https://github.com/b53-clouddevops/cart.git'
                                sh "cd mutable-infra"
                                sh "export TF_VAR_APP_VERSION=0.0.5"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                        }
                    }  
                stage('Create Catalogue') {
                    steps {
                        git branch: 'main', url: 'https://github.com/b53-clouddevops/catalogue.git'
                                sh "cd mutable-infra"
                                sh "export TF_VAR_APP_VERSION=0.1.0"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                        }
                    }
                stage('Create User') {
                    steps {
                        git branch: 'main', url: 'https://github.com/b53-clouddevops/user.git'
                                sh "cd mutable-infra"
                                sh "export TF_VAR_APP_VERSION=0.0.3"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                        }
                    }
                stage('Create Shipping') {
                    steps {
                        git branch: 'main', url: 'https://github.com/b53-clouddevops/shipping.git'
                                sh "cd mutable-infra"
                                sh "export TF_VAR_APP_VERSION=0.0.1"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                        }
                    }
                stage('Create Payment') {
                    steps {
                        git branch: 'main', url: 'https://github.com/b53-clouddevops/payment.git'
                                sh "cd mutable-infra"
                                sh "export TF_VAR_APP_VERSION=0.0.1"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                        }
                    }
                stage('Create Frontend') {
                    steps {
                        git branch: 'main', url: 'https://github.com/b53-clouddevops/frontend.git'
                                sh "cd mutable-infra"
                                sh "export TF_VAR_APP_VERSION=0.0.1"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                        }
                    }
                }    
            }                        
        }
    }

