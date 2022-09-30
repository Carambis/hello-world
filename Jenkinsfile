pipeline {
    agent any
    environment {
        HUB_CREDS = credentials('8671df90-36e3-4dab-9cc4-e92caf77602a')
    }
    stages {
        stage('Build') {
            steps {
                git 'https://github.com/Carambis/hello-world'
                sh "docker build -t hello-world:${env.BUILD_ID} ."
            }
        }
        stage('Push') {
            steps {
                sh "docker login --username=$HUB_CREDS_USR --password=$HUB_CREDS_PSW"
                sh "docker tag hello-world:${env.BUILD_ID} carambis/hello-world:${env.BUILD_ID}"
                sh "docker tag hello-world:${env.BUILD_ID} carambis/hello-world:latest"
                sh "docker push carambis/hello-world:${env.BUILD_ID}"
                sh "docker push carambis/hello-world:latest"
            }
        }
        stage('Publish') {
            steps {
                withKubeConfig([credentialsId: 'test']) {
                     sh "kubectl apply -f hello-world-service.yaml"
                }
            }
        }
    }
}