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
                deploy adapters: [tomcat9(credentialsId: 'tomcat-server', path: '', url: 'http://192.168.1.12:8081/')], contextPath: null, war: '**/*.war'war: '**/*.war'
            }
        }
    }
}
