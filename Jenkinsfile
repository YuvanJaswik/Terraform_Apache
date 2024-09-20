pipeline {
    agent any
     
    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
     }
        stages {
         stage ('Git Checkout') {
                   steps {
                     git branch: 'main', url: 'https://github.com/YuvanJaswik/Terraform_Apache.git'
                     }
                  }
           stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform Plan') {
            steps {
                sh 'terraform plan'
            }
        }
        
        stage('Execute Action') {
            steps {
                script {
                    if (params.ACTION == 'apply') {
                        echo 'Applying changes...'
                        sh 'terraform apply -auto-approve'
                    } else if (params.ACTION == 'destroy') {
                        echo 'Destroying resources...'
                        sh 'terraform destroy -auto-approve'
                    }
                }
            }
         }
    }
}
