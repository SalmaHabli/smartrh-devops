pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SalmaHabli/smartrh-devops.git'
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
