

pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/bayuketah/nginx-jenkins-pipeline.git'
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh 'kubectl apply -f nginx-deployment.yml'
            }
        }
    }
}

