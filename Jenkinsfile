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

        stage('Docker Build') {
            steps {
                bat 'docker build -t java-devops-project .'
            }
        }

        stage('Docker Tag') {
            steps {
                bat 'docker tag java-devops-project sireesha/java-devops-project:latest'
            }
        }

        stage('Trivy Scan') {
            steps {
                bat 'D:\\trivy\\trivy.exe image sireesha/java-devops-project:latest'
            }
        }

    }
}