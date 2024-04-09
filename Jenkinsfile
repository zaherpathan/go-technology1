pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/zaherpathan/go-technology1.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('myrepo')
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                sh 'terraform init'
                sh 'terraform apply --auto-approve'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('905418272007.dkr.ecr.us-east-1.amazonaws.com/myrepo:latest', 'docker-credentials-id') {
                        docker.image('myrepo').push('latest')
                    }
                }
            }
        }

  }
