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
                    withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: '', contextName: '', credentialsId: 'da30ff86-bb62-4226-bcea-1af251cd6175', namespace: '', serverUrl: ''], [caCertificate: '', clusterName: '', contextName: '', credentialsId: '0f678a85-4f8e-4a80-ad14-c786bd7e3646', namespace: '', serverUrl: '']])
}
                }
            }
        }
    }
}
