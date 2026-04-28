pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('List files') {
            steps {
                sh 'ls -l'
            }
        }

        stage('Success') {
            steps {
                echo "Pipeline OK ✔️"
            }
        }
    }
}
