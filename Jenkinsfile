pipeline {
    agent {
       label 'java-maven'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '3', artifactNumToKeepStr: '5'))
    }
    stages{
        stage('Build'){
            steps{
                container('global-maven3-jdk8'){              
                    echo '=== Building Petclinic Application ==='
                    sh 'mvn compile'
                }
            }
        }
        stage('Test'){
            steps{
                container('global-maven3-jdk8'){ 
                    echo '=== Testing Petclinic Application ==='
                    sh 'mvn test'
                }
            }
        }
        stage('Package'){
            steps{
                container('global-maven3-jdk8'){ 
                    echo '=== Package Petclinic Application ==='
                    sh 'mvn package'  
                }
            }
        }
        stage('Publish'){
            steps{
                echo '=== Publish Petclinic Application ==='
                
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        always {
            junit 'target/surefire-reports/*.xml'
        }
    }
}
