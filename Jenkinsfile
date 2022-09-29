pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/Carambis/hello-world'
                sh 'docker build -t hello-world-${env.BUILD_ID} .'
            }
        }
    }
}