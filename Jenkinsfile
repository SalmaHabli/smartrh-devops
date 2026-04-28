pipeline {
    agent any

    environment {
        DOCKERHUB_USER = "salma217"
        BACKEND_IMAGE = "smartrh-backend"
        FRONTEND_IMAGE = "smartrh-frontend"
        VERSION = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend') {
            steps {
                sh "docker build -t $DOCKERHUB_USER/$BACKEND_IMAGE:$VERSION ./backend"
            }
        }

        stage('Build Frontend') {
            steps {
                sh "docker build -t $DOCKERHUB_USER/$FRONTEND_IMAGE:$VERSION ./frontend"
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials-id',
                                                  usernameVariable: 'USER',
                                                  passwordVariable: 'PASS')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                }
            }
        }

        stage('Push Images') {
            steps {
                sh "docker push $DOCKERHUB_USER/$BACKEND_IMAGE:$VERSION"
                sh "docker push $DOCKERHUB_USER/$FRONTEND_IMAGE:$VERSION"
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                sh "kubectl apply -f backend-deployment.yaml"
                sh "kubectl apply -f frontend-deployment.yaml"
                sh "kubectl apply -f postgres-deployment.yaml"
                sh "kubectl apply -f backend-service.yaml"
                sh "kubectl apply -f frontend-service.yaml"
            }
        }

        stage('Success') {
            steps {
                echo "🚀 CI/CD Completed Successfully"
            }
        }
    }
}
