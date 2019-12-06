pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
               echo 'Build...'
               sh 'mvn clean'
               sh 'mvn compile'
               archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging...'
                sh 'mvn package'
            }
        }
    }
}