pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR_USERNAME/springboot-helloworld.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
