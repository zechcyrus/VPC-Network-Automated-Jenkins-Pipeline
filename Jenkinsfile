pipeline {
    agent any

    parameters {
        choice(
            name: 'TERRAFORM_ACTION',
            choices: ['apply', 'destroy'],
            description: 'Choose whether to apply or destroy infrastructure'
        )
    }
    
    stage('Checkout') {
    steps {
        git url: 'https://github.com/zechcyrus/VPC-Network-Automated-Jenkins-Pipeline.git', branch: 'Pipeline'
        }
    }

    stages {
        stage('Initialize Terraform') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Plan Infrastructure') {
            steps {
                sh 'terraform plan'
            }
        }

        stage('Execute Terraform Action') {
            steps {
                script {
                    def action = params.TERRAFORM_ACTION
                    if (action == 'apply') {
                        sh 'terraform apply -auto-approve'
                    } else if (action == 'destroy') {
                        sh 'terraform destroy -auto-approve'
                    }
                }
            }
        }
    }
}
