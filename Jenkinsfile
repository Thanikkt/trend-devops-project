pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Thanikkt/trend-devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t trend-devops-app .'
            }
        }

        stage('Tag Image') {
            steps {
                sh 'docker tag trend-devops-app thanikdevops/trend-devops-app:latest'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push thanikdevops/trend-devops-app:latest'
            }
        }

    }
    stage('Deploy to Kubernetes') {
    steps {
        sh 'kubectl apply -f k8s/deployment.yaml'
        sh 'kubectl apply -f k8s/service.yaml'
    }
}
}
