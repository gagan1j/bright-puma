pipeline {
    agent any

    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'refs/heads/main']]])
            }
        }

        stage('Clone Repository') {
            steps {
                git 'https://github.com/gagan1j/bright-puma.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                bat 'python --version'
                bat 'python -m venv venv'
                bat 'call venv\\Scripts\\activate && pip install -r requirements.txt'
            }
        }

        stage('Start Flask Application') {
            steps {
                bat 'call venv\\Scripts\\activate && python app.py'
            }
        }
    }
}

