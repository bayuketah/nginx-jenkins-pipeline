

pipeline {
  agent any
  environment {
    IMAGE_NAME = 'nginx-demo'
    DOCKERHUB_REPO = 'brittanylordes/nginx-demo'
  }
  stages {
    stage('Clone Repo') {
      steps {
        git branch: 'main', url: 'https://github.com/bayuketah/nginx-jenkins-pipeline.git'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $IMAGE_NAME .'
      }
    }
    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
          sh '''
          docker tag $IMAGE_NAME $DOCKERHUB_REPO:latest
          echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin
          docker push $DOCKERHUB_REPO:latest
          '''
        }
      }
    }
    stage('Deploy to EKS') {
      steps {
        sh 'kubectl apply -f nginx-deployment.yaml'
      }
    }
  }
}

