pipeline {
    agent any

stage('Build') {
    steps {
        echo 'Creating virtual environment and installing dependencies...'
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
                sh 'python3 -m unittest discover -s .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application to a mock deployment directory...'
                sh '''
                    mkdir -p "${WORKSPACE}/python-app-deploy"
                    cp app.py requirements.txt "${WORKSPACE}/python-app-deploy/"
                '''
            }
        }

        stage('Run Application') {
            steps {
                echo 'Starting the Flask application...'
                sh '''
                    if [ -f "${WORKSPACE}/python-app-deploy/app.pid" ]; then
                        old_pid=$(cat "${WORKSPACE}/python-app-deploy/app.pid")
                        kill "$old_pid" 2>/dev/null || true
                    fi

                    nohup python3 "${WORKSPACE}/python-app-deploy/app.py" \
                        > "${WORKSPACE}/python-app-deploy/app.log" 2>&1 &
                    echo $! > "${WORKSPACE}/python-app-deploy/app.pid"
                '''
            }
        }

        stage('Test Application') {
            steps {
                echo 'Checking the deployed Flask application...'
                sh '''
                    python3 - <<'PY'
import time
import urllib.request

url = "http://127.0.0.1:5000/"
for attempt in range(15):
    try:
        with urllib.request.urlopen(url, timeout=2) as response:
            body = response.read().decode("utf-8")
            print("HTTP status:", response.status)
            print("Response:", body)
            assert response.status == 200
            assert body == "Hello, Jenkins Multi-Stage Pipeline!"
            break
    except Exception:
        if attempt == 14:
            raise
        time.sleep(1)
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
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}
