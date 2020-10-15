pipeline {
    agent any
    stages {
        stage('Validate Input') {
            steps {
                echo "Input Validated"
            }
        }
        stage('gitSCM') {
            steps {
                echo "Checked Out code from GitHub"
            }
        }
        stage('Build Docker Image and Tag') {
            steps {
                echo "Built and tagged a docker image"
            }
        }
        stage('Publish') {
            steps {
                echo "Published a docker image to Dockerhub"
            }
        }
    }
}
