pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ericvelez28733/Springboot-HelloWorld.git'
            }
        }

        stage('Build') {
            steps {
                withMaven(maven: 'M3') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}

