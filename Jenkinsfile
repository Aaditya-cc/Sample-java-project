pipeline {
    agent {
        docker {
            image ' maven:3.5.0-jdk-8-alpine'
        }
    }
    stages {
        stage('Building our image') {
            steps {
                script {
                    dockerImage = docker.build "aaditya7789/maventest:$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    // Assume the Docker Hub registry by passing an empty string as the first parameter
                    docker.withRegistry('' , 'dockerhub') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}