pipeline {
    agent any

    environment {
        VENV = 'venv'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                echo 'Setting up Python virtual environment...'
                sh '''
                    python3 -m venv $VENV
                    source $VENV/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests with pytest...'
                sh '''
                    source $VENV/bin/activate
                    mkdir -p test-results
                    pytest test_main.py --junitxml=test-results/results.xml
                '''
            }
            post {
                always {
                    junit 'test-results/results.xml'
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh '''
                    source $VENV/bin/activate
                    python setup.py sdist bdist_wheel
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Replace this with your real deployment commands
                sh 'echo "Deploy step placeholder"'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
            // Add notification steps here if needed (email, Slack, etc)
        }
    }
}

