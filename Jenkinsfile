pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
               echo 'Build...'
               sh 'mvn clean'
               sh 'mvn compile'
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
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage('Analyse') {
            steps {
                echo 'Analyse...'
                sh 'mvn checkstyle:checkstyle'
                sh 'mvn spotbugs:spotbugs'
            }
        }
    }
    post {
        always {
            junit '**/surefire-reports/*.xml' }
    }
}