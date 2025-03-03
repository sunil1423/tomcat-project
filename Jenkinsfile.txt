@Library('shared-libe') _
pipeline{
    agent any

    stages{
        stage('Hello'){
            steps{
                echo 'Hello sunil'
            }
        }
    }
}
