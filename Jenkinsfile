pipeline {
    agent any

    tools {
        maven 'M3'
    }

    environment {
        NEXUS_URL = "http://localhost:8081/repository/maven-releases/"
        NEXUS_CREDENTIALS = credentials('nexus-creds')
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
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Upload to Nexus') {
            steps {
                sh """
                    curl -v -u ${NEXUS_CREDENTIALS_USR}:${NEXUS_CREDENTIALS_PSW} \
                    --upload-file target/*.jar \
                    ${NEXUS_URL}
                """
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}

