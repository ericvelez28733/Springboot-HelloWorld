pipeline {
    agent any

   stage('Checkout') {
    steps {
        git branch: 'main',
            url: 'https://github.com/ericvelez28733/Springboot-HelloWorld.git'
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

