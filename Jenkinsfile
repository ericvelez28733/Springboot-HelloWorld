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
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Upload to Nexus') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'nexus-creds',
                    usernameVariable: 'NEXUS_USER',
                    passwordVariable: 'NEXUS_PASSWORD'
                )]) {
                    sh """
                        curl -v -u $NEXUS_USER:$NEXUS_PASSWORD \
                        --upload-file target/springboot-helloworld-0.0.1-SNAPSHOT.jar \
                        http://localhost:8081/repository/maven-releases/springboot-helloworld/springboot-helloworld/0.0.1/springboot-helloworld-0.0.1-SNAPSHOT.jar
                    """
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
