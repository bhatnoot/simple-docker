pipeline {
    environment {
        imagename = "bhatnootana/jenkins-docker"
        registryCredential = 'nootana-dockerhub'
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git([url: 'https://github.com/bhatnoot/simple-docker.git', branch: 'main'])
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build imagename
                }
            }
        }
        stage('Running image') {
            steps {
                script {
                    sh "docker run -d --name my_container ${imagename}:latest"
                }
            }
        }
        stage('Deploy Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push("$BUILD_NUMBER")
                        dockerImage.push('latest')
                    }
                }
            }
        }
        stage('Pull and Run Docker Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        docker.image(imagename).pull("$BUILD_NUMBER")
                        docker.image(imagename).pull('latest')
                    }
                    sh "docker run -d --name my_container ${imagename}:latest"
                }
            }
        }
    }
}
