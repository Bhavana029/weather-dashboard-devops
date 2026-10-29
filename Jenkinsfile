```groovy
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

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t weather-dashboard:v1 .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKERHUB_USER',
                        passwordVariable: 'DOCKERHUB_TOKEN'
                    )
                ]) {
                    sh '''
                        echo "$DOCKERHUB_TOKEN" | docker login \
                            -u "$DOCKERHUB_USER" --password-stdin

                        docker tag weather-dashboard:v1 \
                            "$DOCKERHUB_USER/weather-dashboard-devops:v1"

                        docker push \
                            "$DOCKERHUB_USER/weather-dashboard-devops:v1"

                        docker logout
                    '''
                }
            }
        }
    }
}
```