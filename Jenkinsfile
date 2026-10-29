
pipeline {
    agent any

    stages {
        stage('Welcome') {
            steps {
                echo 'Weather Dashboard CI/CD'
            }
        }

        stage('Check Environment') {
            steps {
                sh 'whoami'
                sh 'git --version'
                sh 'docker --version'
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t weather-dashboard:v1 .'
            }
        }
    }
}
