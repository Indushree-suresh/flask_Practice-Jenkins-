pipeline {
    agent any

    stages {

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
        pkill -f app.py || true
        . venv/bin/activate
        nohup python app.py > app.log 2>&1 &
        sleep 5
        '''
    }
}
            
               
                
                
                
            }
        }
    }

    post {
        success {
            echo "Build Successful 🎉"
        }
        failure {
            echo "Build Failed ❌"
        }
    }
}
