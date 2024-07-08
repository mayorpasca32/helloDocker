pipeline {
    agent any

    stages {
        stage('Checkout GitHub repo') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mayorpasca32/helloDocker.git']])
            }
        }
        
        stage('Build and Tag Docker Image') {
            steps {
                script {
                    sh 'docker build . -t mayorpasca32/hellodocker'
                    sh 'docker tag hellodocker mayorpasca32/hellodocker:latest'
                }
            }
        }
        
        stage('Push the Docker Image to DockerHUb') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'docker_hub', variable: 'docker_hub')]) {
                    sh 'docker login -u mayorpasca32 -p ${docker_hub}'
}
                    sh 'docker push mayorpasca32/hellodocker'
                }
            }
        }
        
        stage('Deploy deployment and service file') {
            steps {
                script {
                    kubernetesDeploy configs: 'deploymentsvc.yaml', kubeconfigId: 'kubernetes_config'
}
                }
            }
        }
    }
}
