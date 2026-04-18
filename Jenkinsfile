pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Set up Python') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh '. venv/bin/activate && pytest test_calculator.py -v'
            }
        }

        stage('Snyk Security Scan') {
            steps {
                sh 'pip install snyk'
                sh 'snyk auth $SNYK_TOKEN'
                sh 'snyk test --severity-threshold=high'
            }
            environment {
                SNYK_TOKEN = credentials('snyk-token')
            }
        }
    }

    post {
        success {
            echo 'Pipeline passed! All tests and security checks cleared.'
        }
        failure {
            echo 'Pipeline failed! Check the logs above.'
        }
    }
}