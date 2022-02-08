pipeline {
    agent {label 'slave'}
    tools {
        maven 'maven'
    }
    
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage ('Scan') {
            steps {
               withSonarQubeEnv(installationName: 'sonarqube', credentialsId: 'sonarqube') {
                sh 'mvn sonar:sonar'
                }
            }
       } 
    }
}
