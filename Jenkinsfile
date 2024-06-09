pipeline{
    agent any
    stages{
        stage("checkout github repo"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Vishaljainhk/dockerdemo.git']])
            }
        }
        stage('build and tag docker image'){
            steps{
                script{
                    sh 'docker build . -t hellodocker'
                    sh 'docker tag hellodocker vishaljainhk/learning'
                }
            }
        }
        stage('push the docker image to docherhub'){
             steps {
                script {
                    withCredentials([string(credentialsId: 'docker_hub', variable: 'docker_hub')]) {
                    sh 'docker login -u vishaljainhk31@gmail.com -p ${docker_hub}'
}
                    sh 'docker push vishaljainhk/learning'
                }
            }
        }
        
        stage('Deploy deployment and service file') {
            steps {
                script {
                    kubernetesDeploy configs: 'deploymentsvc.yaml', kubeconfigId: 'k8_auth'
                }
            }
        } 
        }
    }

