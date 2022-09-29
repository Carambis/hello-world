pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/Carambis/hello-world'
                sh "docker build -t hello-world-${env.BUILD_ID} ."
            }
        }
        stage('Push') {
            steps {
                sh "docker login --username=Carambis --email=lepeshko1997@gmail.com"
                sh "docker push Carambis/hello-world-${env.BUILD_ID}"
            }
        }
    }
}