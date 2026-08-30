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
                sh 'docker build -t devops-web-app:${BUILD_NUMBER} ./app'
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
                        devops-web-app:${BUILD_NUMBER}
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                    for i in {1..10}; do
                        if curl --fail http://devops-web-app:80; then
                            echo "Health check passed!"
                            exit 0
                        fi
                        echo "Application not ready yet. Retrying..."
                        sleep 2
                    done

                    echo "Health check failed."
                    exit 1
                '''
            }
        }
    }
}
