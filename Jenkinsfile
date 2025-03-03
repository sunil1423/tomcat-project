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
                withCredentials([usernamePassword(credentialsId: 'tomcat-server', usernameVariable: 'sunil123', passwordVariable: 'sunil123')]) {
                    deploy adapters: [
                        tomcat7(
                            path: '',
                            url: 'http://192.168.1.12:8081/manager/text', // Adjust the URL if needed
                            username: "${sunil123}",
                            password: "${sunil123}"
                        )
                    ], war: '**/*.war', contextPath: 'ai-enterprises'
                }
            }
        }
    }
}
