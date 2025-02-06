pipeline {
    agent any
    environment {
        VENV_DIR = 'venv'  // Virtual Environment Directory
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/gagan1j/bright-puma.git'
            }
        }
        stage('Setup Python Environment') {
            steps {
                sh 'python3 -m venv $VENV_DIR'
                sh 'source $VENV_DIR/bin/activate && pip install -r requirements.txt'
            }
        }
        stage('Run Unit Tests') {
            steps {
                sh 'source $VENV_DIR/bin/activate && pytest tests/'  // Run tests (if available)
            }
        }
        stage('Start Flask Application') {
            steps {
                sh 'source $VENV_DIR/bin/activate && nohup python3 app.py &'
            }
        }
    }
}

