
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

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f cloud-app || true
                    docker run -d --name cloud-app -p 5000:5000 cloud-app
                '''
            }
        }
    }
}
