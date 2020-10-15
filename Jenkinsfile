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
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/okuswaha/maven-tool.git']]])
                echo "Checked Out code from GitHub"
            }
        }
        stage('Build Docker Image and Tag') {
            steps {
                withDockerRegistry(credentialsId: 'dockerhub-okuswaha', url: 'https://hub.docker.com/repository/docker/okuswaha/maven-tool') {
                    def customImage = docker.build('maven-tool')
                    customImage.push("latest")
                    sh "docker rmi --force \$(docker images -q ${customImage.id} | uniq)"
}
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
