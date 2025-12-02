pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/zaborowskia1-stack/springboot-mysql-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }

        stage('Upload to Nexus') {
            steps {
                sh """
                mvn deploy -DaltDeploymentRepository=nexus::default::http://nexus-service:8081/repository/maven-snapshots/
                """
            }
        }
    }
}
