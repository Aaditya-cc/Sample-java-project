pipeline {
    agent {
        docker {
            image 'maven:3.8.1-adoptopenjdk-11'
            label 'my-defined-label'
            args  '-v /tmp:/tmp'
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