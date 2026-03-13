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
                bat 'docker tag java-devops-project sirireddyyanamala/java-devops-project:v%BUILD_NUMBER%'
            }
        }

        stage('Trivy Scan') {
            steps {
                bat 'D:\\trivy.exe image --timeout 10m sirireddyyanamala/java-devops-project:v%BUILD_NUMBER%'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push sirireddyyanamala/java-devops-project:v%BUILD_NUMBER%'
            }
        }

    }
}