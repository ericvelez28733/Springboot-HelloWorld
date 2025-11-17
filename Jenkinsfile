pipeline {
    agent any

    tools {
        maven 'M3'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ericvelez28733/Springboot-HelloWorld.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -version'
                sh 'mvn clean package -DskipTests'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}


