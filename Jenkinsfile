pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }
        
        stage('Lint') {
            steps {
                sh '''
                echo "Running lint..."
                . venv/bin/activate
                flake8 app.py
                '''
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh '''
                echo "Running unit tests..."
                . venv/bin/activate
                pytest test_app.py -v
                '''
            }
        }
        
        stage('Archive Artifact') {
            steps {
                echo "Build complete. Archiving app.py..."
                archiveArtifacts artifacts: 'app.py', fingerprint: true
            }
        }
    }
}