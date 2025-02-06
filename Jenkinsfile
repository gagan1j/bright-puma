pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/gagan1j/bright-puma.git', branch: 'main'
            }
        }
        stage('Setup Python Environment') {
            steps {
                bat 'python --version' // Ensure Python is installed
                bat 'python -m venv venv' // Create virtual env
                bat 'call venv\\Scripts\\activate' // Activate venv
                bat 'pip install -r requirements.txt' // Install dependencies
            }
        }
        stage('Run Unit Tests') {
            steps {
                bat 'call venv\\Scripts\\activate && pytest' // Run tests
            }
        }
        stage('Start Flask Application') {
            steps {
                bat 'start /b python app.py' // Use 'start /b' instead of nohup
            }
        }
    }
}

