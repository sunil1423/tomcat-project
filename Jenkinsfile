pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war', allowEmptyArchive: true
                }
            }
        }
        
         stage('Deploying to tomcat server') {
            steps {
                // Use Jenkins credentials securely for deployment
                withCredentials([usernamePassword(credentialsId: '0a83548d-3fa7-443b-98e2-af8aede35020', usernameVariable: 'admin', passwordVariable: 'admin123')]) {
                    deploy adapters: [
                        tomcat7(
                            path: '',
                            url: 'http://192.168.1.12:8081/manager/text', // Adjust the URL if needed
                            username: "${admin}",
                            password: "${admin123}"
                        )
                    ], war: '**/*.war', contextPath: 'ai-enterprises'
                }
            }
        }
    }
}
