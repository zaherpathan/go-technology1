



aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 905418272007.dkr.ecr.us-east-1.amazonaws.com


docker push 905418272007.dkr.ecr.us-east-1.amazonaws.com/myrepo:latest


zaherpathan
zaherpathan


vi 

FROM python:3.9
WORKDIR /app
COPY your_script.py /app
RUN pip install --no-cache-dir -r requirements.txt
CMD ["python", "./your_script.py"]




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
:wq
[A[C[C