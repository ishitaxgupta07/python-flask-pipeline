
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Installing Python dependencies...'
                sh '''
                    python3 -m venv .venv
                    .venv/bin/python -m pip install --upgrade pip
                    .venv/bin/python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh '.venv/bin/python -m unittest discover -s .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Copying application files...'
                sh '''
                    mkdir -p python-app-deploy
                    cp app.py requirements.txt python-app-deploy/
                '''
            }
        }

        stage('Test Application') {
            steps {
                echo 'Testing the Flask application...'
                sh '''
                    .venv/bin/python - <<'PY'
from app import app

client = app.test_client()
response = client.get("/")

print("HTTP status:", response.status_code)
print("Response:", response.get_data(as_text=True))

assert response.status_code == 200
assert response.get_data(as_text=True) == "Hello, Jenkins Multi-Stage Pipeline!"
print("Application test passed!")
PY
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
