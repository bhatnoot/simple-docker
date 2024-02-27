pipeline {
 environment {
 imagename = “bhatnootana/jenkins-docker”
 registryCredential = ‘nootana-dockerhub’
 dockerImage = ‘’
 }
 agent any
 stages {
 stage(‘Cloning Git’) {
 steps {
 git([url: ‘https://github.com/bhatnoot/simple-docker.git', branch: ‘main’])
 }
 }
 stage(‘Building image’) {
 steps{
 script {
 dockerImage = docker.build imagename
 }
 }
 }
 stage(‘Running image’) {
 steps{
 script {
 sh “docker run ${imagename}:latest”
 }
 }
 }
 stage(‘Deploy Image’) {
 steps{
 script {
 docker.withRegistry( ‘’, registryCredential ) {
 dockerImage.push(“$BUILD_NUMBER”)
 dockerImage.push(‘latest’)
 }
 }
 }
 }
 

		stage('Pull and Run Docker Image') {
            steps {
                script {
                    // Define the Docker image name
                    def imagename = 'bhatnootana/jenkins-docker:tag'
                    
                    // Pull the Docker image
                    sh "docker pull $imagename"
                    
                    // Run the Docker container
                    sh "docker run -d --name my_container $imagename"
                }
            }
        }
 }
}
