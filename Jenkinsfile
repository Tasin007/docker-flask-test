pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('amonkincloud-dockerhub')  // Reference the credentials ID from Jenkins
    }
    stages {
        stage('Build docker image') {
            steps {
                // Build the Docker image using the build number as the tag
                sh 'docker build -t tasin007/flaskapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps {
                // Login to Docker Hub using the stored credentials
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps {
                // Push the Docker image to Docker Hub
                sh 'docker push tasin007/flaskapp:$BUILD_NUMBER'
            }
        }
    }
    post {
        always {
            // Logout from Docker Hub
            sh 'docker logout'
        }
    }
}
