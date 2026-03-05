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
                sh 'docker tag trend-devops-app thanikavel/trend-devops-app:latest'
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push thanikavel/trend-devops-app:latest'
                }
            }
        }

    }
}
