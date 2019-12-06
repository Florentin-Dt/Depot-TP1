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
                sh 'mvn spotBugs:spotBugs'
                sh 'mvn pmd:pmd'
            }
        }
    }
    post {
        always {
            junit '**/surefire-reports/*.xml'
            recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            recordIssues enabledForFailure: true, tool: checkstyle()
            recordIssues enabledForFailure: true, tool: spotBugs()
            recordIssues enabledForFailure: true, tool: cpd(pattern: '**/target/cpd.xml')
            recordIssues enabledForFailure: true, tool: pmdParser(pattern: '**/target/pmd.xml')
         }
    }
}