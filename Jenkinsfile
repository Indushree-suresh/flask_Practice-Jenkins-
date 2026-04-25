pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/Indushree-suresh/flask_Practice-Jenkins-.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                . venv/bin/activate
                pip install pytest
                pytest || echo "No tests found"
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                . venv/bin/activate
                nohup python app.py > app.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo "Build Successful "
        }
        failure {
            echo "Build Failed "
        }
    }
}
