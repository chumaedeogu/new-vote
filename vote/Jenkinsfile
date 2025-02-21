pipeline {
    agent any
    environment {
        IMAGE_NAME = "chumaedeogu/vote"
    }
    stages {
        stage("Log in and Build Docker Image") {
            steps {
                script {
                    def TAG = "${env.BUILD_NUMBER}"
                    sh "docker build -t ${IMAGE_NAME}:latest -t ${IMAGE_NAME}:${TAG} ."
                }
            }
        }
        stage("Push Image to Registry") {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-cred']) {
                    script {
                        def TAG = "${env.BUILD_NUMBER}"
                        sh "docker push ${IMAGE_NAME}:${TAG}"
                    
                    }
                }
            }
        }
    }
}