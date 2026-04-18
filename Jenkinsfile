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
                sh 'apt-get update && apt-get install -y python3 python3-pip python3-venv'
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
            environment {
                SNYK_TOKEN = credentials('snyk-token')
            }
            steps {
                sh '. venv/bin/activate && pip install snyk'
                sh '. venv/bin/activate && snyk auth $SNYK_TOKEN'
                sh '. venv/bin/activate && snyk test --severity-threshold=high'
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