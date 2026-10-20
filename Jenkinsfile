
pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Meet-hue/jenkins-cicd.git'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t cloud-app .'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_TOKEN'
                )]) {
                    sh '''
                        echo "$DOCKER_TOKEN" | docker login \
                            -u "$DOCKER_USER" --password-stdin
                        docker tag cloud-app "$DOCKER_USER/cloud-app:latest"
                        docker push "$DOCKER_USER/cloud-app:latest"
                        docker logout
                    '''
                }
            }
        }

        stage('Deploy on EC2') {
            steps {
                sh '''
                    docker rm -f cloud-app || true
                    docker run -d --name cloud-app \
                        -p 5000:5000 cloud-app
                    sleep 3
                    curl --fail http://localhost:5000
                '''
            }
        }
    }
}
