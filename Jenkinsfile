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
        stage('Publish'){
            steps{
                nexusPublisher nexusInstanceId: 'Nexus_localhost', nexusRepositoryId: 'maven-snapshots', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: "target/word-count-${POM_VERSION}-jar-with-dependencies.jar"]], mavenCoordinate: [artifactId: 'word-count', groupId: 'cicd.learn.tp1', packaging: 'jar', version: "${POM_VERSION}"]]]
            }
        }
    }
    post {
        always {
            junit '**/surefire-reports/*.xml'
            //recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            //recordIssues enabledForFailure: true, tools: [checkStyle(), spotBugs(), cpd(pattern: '**/target/cpd.xml'), pmdParser(pattern: '**/target/pmd.xml')]
            recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            recordIssues enabledForFailure: true, tool: checkStyle()
            recordIssues enabledForFailure: true, tool: spotBugs()
            recordIssues enabledForFailure: true, tool: cpd(pattern: '**/target/cpd.xml')
            recordIssues enabledForFailure: true, tool: pmdParser(pattern: '**/target/pmd.xml')
        }
    }
}