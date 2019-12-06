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
                sh 'mvn site'
                sh 'mvn checkstyle:checkstyle'
                sh 'mvn spotbugs:spotbugs'
                sh 'mvn pmd:pmd'
            }
        }
    }
    post {
        always {
            junit '**/surefire-reports/*.xml'
            recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            recordIssues enabledForFailure: true, tools: [checkStyle(), spotBugs(), cpd(pattern: '**/target/cpd.xml'), pmdParser(pattern: '**/target/pmd.xml')]
         }
    }
}