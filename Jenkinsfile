pipeline {
    agent any

    environment {
        NEXUS_REPO = "http://192.168.49.2:30081/repository/maven-snapshots/"
    }

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

        stage('Deploy to Nexus') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'nexus-admin', usernameVariable: 'NEXUS_USER', passwordVariable: 'NEXUS_PASS')]) {
                    sh """
                        ./mvnw deploy \
                        -DaltDeploymentRepository=snapshots::default::${NEXUS_REPO} \
                        -Dnexus.username=$NEXUS_USER \
                        -Dnexus.password=$NEXUS_PASS
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deploy successful!'
        }
        failure {
            echo 'Something went wrong.'
        }
    }
}
