pipeline {
    environment {
        customImage = ''
    }
    agent any
    stages {
        stage('Validate Input') {
            steps {
                echo "Input Validated"
            }
        }
        stage('Checkout Repo') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/okuswaha/maven-tool.git']]])
                echo "Checked out code from GitHub"
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    customImage = docker.build maven-tool
                    echo "Built a docker image"
                }
            }
        }
        stage('Tag Docker image and publish') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub-okuswaha', url: 'https://hub.docker.com/repository/docker/okuswaha/maven-tool') {
                        customImage.push("latest")
                        sh "docker rmi --force \$(docker images -q ${customImage.id} | uniq)"
                    }
                }
                echo "Tagged and Published a docker image to Dockerhub"
            }
        }
    }
}
