pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Tomcat Server') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'Tomcat_credentials', path: '', url: 'http://localhost:8081/')], 
                contextPath: '', war: '**/target/*.war'
            }
        }
    }
}
