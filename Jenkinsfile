pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-web-app:$BUILD_NUMBER ./app'
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    docker stop devops-web-app || true
                    docker rm devops-web-app || true

                    docker run -d \
                        --name devops-web-app \
                        --network devops-network \
                        -p 8080:80 \
                        devops-web-app:$BUILD_NUMBER
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                    sleep 5
                    curl --fail http://localhost:8080
                '''
            }
        }
    }
}
