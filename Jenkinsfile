pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {

        stage('Build Application') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('Sonarqube') {
                    bat 'mvn sonar:sonar'
                }
            }
        }

    }
}