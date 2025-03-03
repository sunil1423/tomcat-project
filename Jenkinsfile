
pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            post{
                success { echo "Archiving the Artifacts"
                archiveArtifacts artifacts: '**/target/*.war'
            }
            }
        }
        stage('Deploying to tomcat server') {
            steps {
                deploy adapters: [tomcat7(path: '', url: 'http://192.168.1.12:8081/')], contextPath: null, war: '**/*.war'
            
            }
        }
    }
}
}
