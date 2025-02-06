pipeline {
    agent any

    environment {
        VENV_PATH = "venv"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/bright-puma.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                python3 -m venv $VENV_PATH
                source $VENV_PATH/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                source $VENV_PATH/bin/activate
                python -m unittest discover tests
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                source $VENV_PATH/bin/activate
                nohup python app.py > app.log 2>&1 &
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    def response = sh(script: "curl -s -o /dev/null -w '%{http_code}' http://localhost:5000/api/v1/status", returnStdout: true).trim()
                    if (response != '200') {
                        error("Application failed to start!")
                    }
                }
            }
        }
    }

    post {
        always {
            sh 'deactivate || true'
        }
    }
}

